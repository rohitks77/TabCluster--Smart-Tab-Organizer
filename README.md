# 🗂️ TabCluster

A powerful Chrome extension that automatically organizes your browser tabs into color-coded groups based on their domain names.

![Version](https://img.shields.io/badge/version-1.3.0-blue)
![Manifest](https://img.shields.io/badge/manifest-v3-green)
![License](https://img.shields.io/badge/license-MIT-yellow)

---

## ✨ Features

### 📦 Smart Tab Grouping
- **One-click grouping** - Instantly organize all tabs by domain
- **Subdomain handling** - Groups subdomains together (mail.google.com → google.com)
- **Consistent colors** - Same domain always gets the same color
- **Custom rules** - Create your own grouping rules (e.g., group all Google services together)

### ✋ Manual Grouping
- **Select specific tabs** - Choose exactly which tabs to group
- **Custom group names** - Name your groups anything you want
- **Color picker** - Choose from 9 different colors
- **Quick select** - Select all, none, or ungrouped tabs only

### 🔄 Auto-Group New Tabs
- Automatically adds new tabs to existing groups
- Creates new groups when 2+ tabs share a domain
- Skips internal browser pages (new tab, settings, etc.)

### 💾 Session Management
- **Save sessions** - Preserve your current tab arrangement
- **Restore sessions** - Bring back saved tabs with their groups intact
- **Up to 10 sessions** - Keep multiple workspaces saved

### 🎨 Customization Options
- **Color styles**: Colorful, Muted, or Grey
- **Show/hide labels** - Toggle domain names on groups
- **Auto-collapse** - Automatically collapse inactive groups after X minutes
- **Dark mode** - Easy on the eyes

### 🔍 Quick Search
- Search across all open tabs
- Find by title, URL, or domain
- Jump to any tab instantly

### ⌨️ Keyboard Shortcut
- `Ctrl+Shift+G` (Windows/Linux)
- `Cmd+Shift+G` (Mac)
- Toggles group/ungroup all tabs

### 🖱️ Right-Click Menu
- Group all tabs
- Ungroup all tabs
- Group current domain only
- Add domain to custom rule

### 📊 Badge Counter
- Shows total tab count on the extension icon
- Can be toggled on/off

### ❓ Built-in Help
- Click the **?** icon in the footer
- View complete usage guide within the extension
- Auto-detects your OS for correct keyboard shortcuts

---

## 📥 Installation

### From Source (Developer Mode)

1. **Download/Clone** this repository
   ```bash
   git clone https://github.com/yourusername/auto-group-tabs.git
   ```

2. **Open Chrome Extensions**
   - Navigate to `chrome://extensions/`
   - Or Menu → More Tools → Extensions

3. **Enable Developer Mode**
   - Toggle the switch in the top-right corner

4. **Load the Extension**
   - Click "Load unpacked"
   - Select the `auto-group-tabs` folder

5. **Pin the Extension** (optional)
   - Click the puzzle piece icon in Chrome toolbar
   - Pin "Auto Group Tabs by Domain"

---

## 🚀 Usage

### Basic Grouping

1. Click the extension icon in your toolbar
2. Click **"📦 Group"** to organize all tabs by domain
3. Click **"📂 Ungroup"** to remove all groups

### Preview Before Grouping

1. Click the extension icon
2. Click **"👁 Preview"** to see how tabs will be grouped
3. View domains, tab counts, and colors before committing

### Manual Grouping

Create custom groups with specific tabs:

1. Click **"✋ Manual"**
2. Select the tabs you want to group (click on them or use Select All/None/Ungrouped)
3. Enter a group name (optional)
4. Choose a color from the dropdown
5. Click **"Create Group"**

### Custom Rules

Create rules to group multiple domains together:

1. Click **"⚙️ Rules"**
2. Enter a rule name (e.g., "Google")
3. Add domains: `google.com`, `youtube.com`, `gmail.com`
4. Click **"Add Rule"**

Now all Google services will be grouped together!

### Session Management

**Save a Session:**
1. Click **"💾 Sessions"**
2. Enter a session name
3. Click **"💾 Save Current"**

**Restore a Session:**
1. Click **"💾 Sessions"**
2. Find your saved session
3. Click the **"↩️"** restore button

### Settings

| Setting | Description |
|---------|-------------|
| Collapse groups | Collapse all groups except the active one |
| Show labels | Display domain names on group tabs |
| Color style | Choose Colorful, Muted, or Grey |
| Auto-collapse | Collapse inactive groups after X minutes |
| Auto-group | Automatically group new tabs |
| Show badge | Display tab count on extension icon |
| Dark mode | Toggle dark theme |

---

## 🎨 Color Palette

The extension uses Chrome's built-in tab group colors:

| Color | Example |
|-------|---------|
| 🔵 Blue | Various domains |
| 🔴 Red | Various domains |
| 🟡 Yellow | Various domains |
| 🟢 Green | Various domains |
| 🩷 Pink | Various domains |
| 🟣 Purple | Various domains |
| 🩵 Cyan | Various domains |
| 🟠 Orange | Various domains |
| ⚫ Grey | Muted mode / fallback |

Colors are assigned consistently using a hash algorithm - the same domain always gets the same color!

---

## 📁 File Structure

```
auto-group-tabs/
├── manifest.json      # Extension configuration (Manifest V3)
├── background.js      # Service worker (core logic)
├── popup.html         # Extension popup UI
├── popup.js           # Popup interactions
├── popup.css          # Popup styling with dark mode
├── icons/
│   ├── icon16.png     # Toolbar icon (16x16)
│   ├── icon48.png     # Extension page icon (48x48)
│   └── icon128.png    # Chrome Web Store icon (128x128)
└── README.md          # Documentation
```

---

## 🔧 Technical Details

### Manifest V3
This extension uses Chrome's latest Manifest V3 format with:
- Service worker architecture (background.js)
- Promise-based Chrome APIs
- Minimal permissions model

### Permissions Used

| Permission | Purpose |
|------------|---------|
| `tabs` | Access tab information (URLs, titles) |
| `tabGroups` | Create and manage tab groups |
| `storage` | Save preferences and sessions locally |
| `contextMenus` | Right-click menu options |
| `alarms` | Auto-collapse timer functionality |

### API Usage

```javascript
// Tab Operations
chrome.tabs.query()      // Get all tabs
chrome.tabs.group()      // Create tab groups
chrome.tabs.ungroup()    // Remove from groups
chrome.tabs.create()     // Create new tabs
chrome.tabs.update()     // Activate tabs

// Tab Group Operations
chrome.tabGroups.query()   // Get all groups
chrome.tabGroups.update()  // Update group properties

// Storage
chrome.storage.local.get()  // Read preferences
chrome.storage.local.set()  // Save preferences

// Other
chrome.alarms.create()      // Set timers
chrome.contextMenus.create() // Create menus
```

### Data Storage Schema

```javascript
// User Preferences
{
  collapseGroups: boolean,      // Collapse after grouping
  showNames: boolean,           // Show domain labels
  colorStyle: string,           // 'colorful' | 'muted' | 'grey'
  autoCollapseEnabled: boolean, // Enable auto-collapse
  autoCollapseMinutes: number,  // Minutes before collapse
  autoGroupNew: boolean,        // Auto-group new tabs
  showBadge: boolean,           // Show tab count badge
  darkMode: boolean             // Dark theme
}

// Custom Grouping Rules
{
  customRules: {
    "RuleName": ["domain1.com", "domain2.com", ...]
  }
}

// Saved Sessions
{
  savedSessions: [
    {
      id: string,           // Unique ID (timestamp)
      name: string,         // User-defined name
      createdAt: string,    // ISO date string
      tabs: [{
        url: string,
        title: string,
        groupId: number,
        pinned: boolean
      }],
      groups: [{
        id: number,
        title: string,
        color: string,
        collapsed: boolean
      }],
      tabCount: number,
      groupCount: number
    }
  ]
}
```

---

## 🐛 Troubleshooting

### Extension icon not showing
1. Go to `chrome://extensions/`
2. Click the refresh button on the extension card
3. Verify PNG icons exist in the `icons/` folder
4. Chrome requires PNG format (not SVG)

### Groups not being created
1. Ensure you have tabs from the same domain
2. Special pages (chrome://, about:, file://) cannot be grouped
3. Single tabs won't create a group (need 2+ from same domain)
4. Try reloading the extension

### Auto-group not working
1. Enable "Auto-group new tabs" in settings
2. Wait for pages to fully load before grouping occurs
3. New tab pages are intentionally skipped
4. Check service worker console for errors

### Sessions not restoring correctly
1. Ensure the original session was saved with grouped tabs
2. Some URLs (chrome://, extension pages) won't be restored
3. Check browser console for specific errors

### How to view debug logs
1. Go to `chrome://extensions/`
2. Find "Auto Group Tabs by Domain"
3. Click "Service Worker" link under the extension
4. DevTools opens - view Console tab for logs

### Reset extension data
```javascript
// Run in extension's service worker console
chrome.storage.local.clear(() => console.log('Data cleared'));
```

---

## 🔄 Changelog

### v1.2.0 (Latest)
- ✨ Added dark mode toggle
- ✨ Added save/restore sessions feature
- ✨ Added auto-group new tabs option
- ✨ Added badge counter for tab count
- 🐛 Fixed context menu errors ('tab' context)
- 🐛 Fixed session restore grouping
- 🐛 Fixed tabs.group() windowId parameter

### v1.1.0
- ✨ Added custom domain rules
- ✨ Added quick search functionality
- ✨ Added auto-collapse timer
- ✨ Added right-click context menu
- 🎨 Redesigned to minimalist UI
- 🐛 Fixed various grouping bugs

### v1.0.0
- 🎉 Initial release
- 📦 Basic tab grouping by domain
- 🎨 Consistent domain-based colors
- 👁 Preview mode
- ⌨️ Keyboard shortcut (Ctrl+Shift+G)

---

## 📝 License

MIT License

Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 💡 Tips & Tricks

| Tip | Description |
|-----|-------------|
| ⌨️ Quick toggle | Use `Ctrl+Shift+G` to instantly group/ungroup |
| 🎯 Focus mode | Enable auto-collapse to keep only active group visible |
| 💼 Work contexts | Save different sessions for different projects |
| 🔗 Related sites | Create custom rules for related websites |
| 🎨 Clean look | Use "grey" color style for minimal distraction |
| 🔍 Fast search | Use the search bar to jump to any tab quickly |

---

## 📊 Browser Compatibility

| Browser | Supported | Notes |
|---------|-----------|-------|
| Chrome | ✅ Yes | Full support (v89+) |
| Edge | ✅ Yes | Full support (Chromium-based) |
| Brave | ✅ Yes | Full support |
| Opera | ✅ Yes | Full support |
| Firefox | ❌ No | Uses different tab groups API |
| Safari | ❌ No | No tab groups API |

---

## 🙏 Acknowledgments

- Chrome Extensions API documentation
- Tab Groups API for making this possible
- All users who provide feedback and suggestions

---

<div align="center">

Made with ❤️ for tab hoarders everywhere

**[Report Bug](../../issues) · [Request Feature](../../issues)**

</div>
