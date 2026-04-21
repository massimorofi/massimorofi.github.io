# Personal Blog ... MaX

# Info
The blog has been developed on top of GiHub Pages, cloning and modifying the [HuxPro Blog Template](https://github.com/Huxpro/huxpro.github.io).


Read [](file:///home/briggen/Dev/code/github/massimorofi.github.io/README.md)

Read [](file:///home/briggen/Dev/code/github/massimorofi.github.io/README.md#7-7), lines 7 to 7

Read [](file:///home/briggen/Dev/code/github/massimorofi.github.io/package.json)

Ran terminal command:  bundle install

Ran terminal command:  npm install
Completed with input:  npm install

Ran terminal command:  npm install --legacy-peer-deps

Ran terminal command:  npm run start

Ran terminal command:  curl -s "http://localhost:4000/2026/04/21/MCP-Gateway-Enterprise-Building-Blocks/" | grep -c "mermaid"

## 🎉 **Your Blog is Now Running Locally!**

### **Access Your Blog:**
- **Main Site**: http://localhost:4000
- **MCP Gateway Article**: http://localhost:4000/2026/04/21/MCP-Gateway-Enterprise-Building-Blocks/
- **LiveReload**: http://localhost:35729 (auto-refreshes on file changes)

### **Key Features Working:**
- ✅ **Mermaid Diagrams**: All 4 diagrams in your MCP Gateway article are rendering
- ✅ **LiveReload**: Changes to files automatically refresh the browser
- ✅ **Full Jekyll Features**: Posts, pages, RSS feed, etc.

### **Development Workflow:**

#### **Option 1: Quick Development (Recommended)**
```bash
npm run dev  # Runs both Jekyll + LESS watcher
```

#### **Option 2: Manual LESS Compilation**
When you modify hux-blog.less:
```bash
npx grunt less  # Compile LESS to CSS
```

#### **Option 3: Stop the Server**
```bash
# In another terminal:
pkill -f "jekyll serve"
```

### **File Structure Overview:**
```
├── _posts/           # Your blog articles (Markdown)
├── _includes/        # Reusable HTML components
├── _layouts/         # Page templates
├── css/             # Compiled stylesheets
├── less/            # LESS source files
├── js/              # JavaScript files
├── _config.yml      # Jekyll configuration
└── _site/           # Generated site (auto-created)
```

### **Making Changes:**
1. **Edit posts**: Modify files in _posts
2. **Edit styles**: Change hux-blog.less then run `grunt less`
3. **Edit layout**: Modify files in _includes or _layouts
4. **Browser auto-refreshes** on changes!



