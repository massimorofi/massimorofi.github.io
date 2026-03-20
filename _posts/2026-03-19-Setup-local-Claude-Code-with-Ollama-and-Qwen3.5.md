---
layout: post
title: 'Mastering Local AI Agents: A Complete Guide to Setting Up Claude Code with Ollama & Qwen 3.5'
date: '2026-03-19T16:40:00.000-08:00'
author: MaX
tags:
- Anthropic
- Claude Code
- Development
- Containers
- Docker
- AI
- Chat
- LLM
- llama
- LocalAI
- AI Agents
modified_time: '2026-03-19T16:40:00.000-08:00'
thumbnail: /img/in-post/OpenAI_Client_Post.png
---

# Mastering Local AI Agents: A Complete Guide to Setting Up Claude Code with Ollama & Qwen 3.5
![OpenAI Cleint Python](/img/in-post/Claude_Code_Setup_Ollama_Qwen3.5.png)
The dream of a fully agentic developer workflow running entirely on your local machine is finally viable. Tools like Anthropic’s **Claude Code** (the CLI for Claude) are incredible, but they require a "smart" backend capable of handling deep context. While cloud models are easy, running **Ollama** and high-performance models like **Qwen 3.5:9b** inside **Docker** offers privacy and zero latency.

However, the default configurations for local models are often tuned for simple chat, not agentic reasoning. If you have tried to link them and found that Claude Code constantly truncates its own responses or fails mid-tool call, you need a specialized setup.

This article provides a complete walkthrough for installing Claude Code and configuring it to use a local, high-context Qwen 3.5 backend. We will also solve the critical "No Modelfile found" error that occurs when customizing Ollama inside a Docker container.


## 1. Prerequisites

Before we begin, ensure your local environment meets the minimum requirements for a 9-billion parameter model with a large context window:

* **Hardware:** 16GB RAM (32GB+ highly recommended).
* **GPU:** An NVIDIA GPU with 8GB+ VRAM (or Apple Silicon Mac) is essential for acceptable performance.
* **Software:** Docker Desktop/Engine, Node.js (v18+) and `npm` installed.

---

## 2. Step 1: Install Claude Code

Claude Code is distributed as a global npm package. This tool must run on your **host machine**, where it can access your local file system and `git` repositories.

Open your terminal and run:

```bash
npm install -g @anthropic-ai/claude-code
```

---

## 3. Step 2: Creating the High-Context Qwen Agent

A standard `ollama pull qwen3.5:9b` is often insufficient for agentic tasks because Ollama defaults to a **4,096 token context window (`num_ctx`)**. Claude Code sends a massive initial system prompt and your directory structure with every request; 4k tokens will be exhausted instantly, leading to truncation.

### The Problem: Docker Isolation
If your Ollama instance is in Docker and your `Modelfile` is in your current local directory, running `ollama create` inside the container will fail with:
> `Error: no Modelfile or safetensors files found`

### The Solution: The "Pipe Trick"
We can bypass this isolation by "piping" the file content directly into the container's standard input.

1.  **Pull the Base Model (inside the container):**
    ```bash
    docker exec -it <your_ollama_container_name> ollama pull qwen3.5:9b
    ``` 

2.  **Create your `Modelfile` (on your host machine):**
    Create a file named `Modelfile` in your current directory with these parameters:

    ```dockerfile
    # High-Context Modelfile for Claude Code
    FROM qwen3.5:9b

    # CRITICAL: Increase context window (64k is recommended for Qwen)
    PARAMETER num_ctx 65536

    # Prevents the model from truncating its own output early
    PARAMETER num_predict -1
    ```

3.  **Run the Create Command:**
    The `-f -` flag tells Ollama to read the definition from the pipe instead of a local path.

    ```bash
    cat Modelfile | docker exec -i <your_ollama_container_name> ollama create qwen-agent -f -
    ```
    or you can use the Docker copy command:

    ```bash    
    docker cp Modelfile <your_ollama_container_name>:/tmp/Modelfile
    ```
---

## 4. Step 3: Configure Claude Code Environment

Claude Code needs to be directed to your Docker endpoint and told to use the new `qwen-agent` model. Since Ollama is in Docker, use the `host.docker.internal` bridge.

Set these environment variables in your terminal (or add them to your `.zshrc` / `.bashrc`):

| Variable | Value | Why? |
| :--- | :--- | :--- |
| **`ANTHROPIC_BASE_URL`** | `http://host.docker.internal:11434/v1` | Points Claude to the internal Docker API bridge. |
| **`ANTHROPIC_API_KEY`** | `ollama` | Local endpoints don't need a key, but the client requires a placeholder. |
| **`CLAUDE_CODE_MAX_OUTPUT_TOKENS`** | `8192` | Prevents the client from cutting off large code blocks. |

```bash
export ANTHROPIC_BASE_URL="[http://host.docker.internal:11434/v1](http://host.docker.internal:11434/v1)"
export ANTHROPIC_API_KEY="ollama"
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=8192
```

---

## 5. Step 4: Launching Your Local Agent

Navigate to the root of your project (ideally a `git` repo) and launch Claude Code:

```bash
claude --model qwen-agent --dangerously-skip-permissions
```

### Why `--dangerously-skip-permissions`?
For a truly agentic experience, the model needs to run commands and read files without asking for your approval every 5 seconds. Use this only in trusted, local environments.

---

## Summary Checklist for Troubleshooting

1.  **Check Context:** Run `ollama show qwen-agent` and confirm `num_ctx` is set to `65536`.
2.  **Monitor VRAM:** A 64k context window consumes significantly more VRAM. If the model becomes extremely slow or crashes, you may need to lower `num_ctx` to `32768`.
3.  **Refresh:** If the model starts acting "confused" after a long session, type `/clear` in Claude Code to reset the history and free up the context window.
4.  **Chek GPU Usage** Use Ollama command to check GPU usage. Example:
```bash
   docker exec -it ollama ollama ps
    NAME                 ID              SIZE     PROCESSOR          CONTEXT    UNTIL   
    qwen-agent:latest    8975289df185    12 GB    56%/44% CPU/GPU    65536      Forever 
```
## GPU Tip
If you are not using the GPU read my previous article on how to setup a loca Ollama Docker container leveraging the GPU processing.
[https://massimorofi.com/2026/01/03/OpenAI-Client-Example-Python/](https://massimorofi.com/2026/01/03/OpenAI-Client-Example-Python/)
