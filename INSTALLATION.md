# Amazon Vine Explorer - Installation Guide

## Table of Contents
1. [Browser Requirements](#browser-requirements)
2. [Installing Tampermonkey](#installing-tampermonkey)
3. [Installing Amazon Vine Explorer](#installing-amazon-vine-explorer)
4. [Verification](#verification)
5. [Updating](#updating)
6. [Uninstalling](#uninstalling)
7. [Troubleshooting](#troubleshooting)

## Browser Requirements

Amazon Vine Explorer works on:

### Desktop Browsers
- ✅ **Google Chrome** (recommended) - Version 90+
- ✅ **Mozilla Firefox** - Version 88+
- ✅ **Microsoft Edge** (Chromium-based) - Version 90+
- ✅ **Opera** - Version 76+
- ✅ **Brave** - Recent versions
- ⚠️ **Safari** - Limited support (Tampermonkey beta required)

### Mobile Browsers
- ⚠️ Limited support on mobile browsers
- Firefox Mobile with Tampermonkey may work
- Not recommended for primary use

## Installing Tampermonkey

Tampermonkey is a browser extension that runs userscripts like Amazon Vine Explorer.

### Chrome / Edge / Opera / Brave

1. **Visit the Chrome Web Store:**
   - Go to: [Tampermonkey on Chrome Web Store](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)

2. **Click "Add to Chrome"** (or "Add to Edge", etc.)

3. **Confirm the installation**
   - Click "Add extension" in the popup

4. **Verify installation**
   - Look for the Tampermonkey icon in your browser toolbar
   - It looks like: 🔲 (a square with circles)

### Firefox

1. **Visit Firefox Add-ons:**
   - Go to: [Tampermonkey on Firefox Add-ons](https://addons.mozilla.org/en-US/firefox/addon/tampermonkey/)

2. **Click "Add to Firefox"**

3. **Confirm the installation**
   - Click "Add" in the popup

4. **Grant permissions**
   - Allow Tampermonkey to access websites when prompted

5. **Verify installation**
   - Look for the Tampermonkey icon in your toolbar

### Safari

1. **Note:** Safari support is limited and requires Tampermonkey Beta

2. **Download Tampermonkey:**
   - Visit: [Tampermonkey for Safari](https://www.tampermonkey.net/?browser=safari)

3. **Follow Safari-specific installation steps**

4. **Grant necessary permissions** in Safari settings

## Installing Amazon Vine Explorer

### Method 1: Direct Install (Recommended)

1. **Ensure Tampermonkey is installed** (see above)

2. **Click the installation link:**
    - **From GitHub (latest stable):**
       ```
       https://raw.githubusercontent.com/matziq/AmazonVineExplorer/i18n/english-ui/VineExplorer.user.js
       ```
   - Click the link or copy-paste it into your browser

3. **Tampermonkey will detect the script:**
   - You'll see the Tampermonkey installation page
   - Review the script details and permissions

4. **Click "Install"**

5. **Confirmation:**
   - You should see "VineExplorer installed"
   - The script is now active

### Method 2: Manual Installation

1. **Get the script code:**
   - Visit: [VineExplorer.user.js on GitHub](https://github.com/matziq/AmazonVineExplorer/blob/i18n/english-ui/VineExplorer.user.js)
   - Click the "Raw" button
   - Copy all the code (Ctrl+A, Ctrl+C)

2. **Open Tampermonkey Dashboard:**
   - Click the Tampermonkey icon in your browser
   - Select "Dashboard"

3. **Create new script:**
   - Click the ➕ (plus) icon or "Create a new script" tab

4. **Paste the code:**
   - Delete any placeholder code
   - Paste the copied script code
   - Press Ctrl+S or click File → Save

5. **Script is now installed**

### Method 3: Install from Fork

If you want the English UI version (or other fork):

1. **Navigate to the fork:**
   - For English UI: `https://raw.githubusercontent.com/matziq/AmazonVineExplorer/i18n/english-ui/VineExplorer.user.js`

2. **Follow Method 1 steps** with the fork URL

## Verification

### Verify Installation

1. **Check Tampermonkey Dashboard:**
   - Click Tampermonkey icon
   - Select "Dashboard"
   - You should see "Amazon Vine Explorer" listed
   - Status should show "Enabled" with a green checkmark

2. **Visit Amazon Vine:**
   - Go to your Amazon Vine page:
     - US: https://www.amazon.com/vine/
     - DE: https://www.amazon.de/vine/
     - UK: https://www.amazon.co.uk/vine/

3. **Look for AVE features:**
   - New buttons on the left side of the page
   - Settings gear icon (⚙️) in navigation
   - "AVE" branding in bottom-left corner
   - Enhanced product tiles with color borders

4. **Test basic functionality:**
   - Click the ⚙️ Settings button
   - Settings panel should open
   - Click "🆕 New Products" button
   - Should see product catalog

### Check Script Version

1. **Open Tampermonkey Dashboard**
2. **Find "Amazon Vine Explorer"**
3. **Version shown in the list** (should match latest release)
4. **Or check in script settings:**
   - Edit the script
   - Look for `@version` in the metadata header

## Updating

### Automatic Updates (Recommended)

Tampermonkey automatically checks for updates if configured:

1. **Open Tampermonkey Settings:**
   - Click Tampermonkey icon
   - Select "Dashboard"
   - Click "Settings" tab

2. **Verify update settings:**
   - "Check interval" should be set (e.g., "Daily")
   - "Check for updates" should be enabled

3. **Scripts will auto-update** when new versions are published

### Manual Update

1. **Open Tampermonkey Dashboard**

2. **Find "Amazon Vine Explorer"**

3. **Click the script name** to edit

4. **Go to script settings (tab/button)**

5. **Check for updates:**
   - Look for "Last updated" timestamp
   - Click "Check for updates now" if available

6. **Or reinstall:**
   - Delete old version
   - Follow installation steps again

### Update from Fork

If using a fork (like the English UI version):

1. **The `@updateURL` in the script** determines where updates come from

2. **To switch update source:**
   - Edit the script in Tampermonkey
   - Find `@updateURL` and `@downloadURL` lines
   - Change to desired repository URL
   - Save

3. **Example URLs:**
   ```javascript
   // Main repository
   // @updateURL https://raw.githubusercontent.com/matziq/AmazonVineExplorer/i18n/english-ui/VineExplorer.user.js
   
   // English UI fork
   // @updateURL https://raw.githubusercontent.com/matziq/AmazonVineExplorer/i18n/english-ui/VineExplorer.user.js
   ```

## Uninstalling

### Remove Amazon Vine Explorer Only

1. **Open Tampermonkey Dashboard:**
   - Click Tampermonkey icon → Dashboard

2. **Find "Amazon Vine Explorer"**

3. **Click the trash/delete icon** (🗑️)

4. **Confirm deletion**

5. **Script is removed**
   - Your browser database remains (see below)

### Remove Tampermonkey Completely

1. **Remove the extension:**
   - **Chrome/Edge:** 
     - Go to `chrome://extensions/` or `edge://extensions/`
     - Find Tampermonkey
     - Click "Remove"
   - **Firefox:**
     - Go to `about:addons`
     - Find Tampermonkey
     - Click "Remove"

2. **This removes all userscripts and settings**

### Clear Amazon Vine Explorer Data

The script stores data in your browser's IndexedDB:

1. **Open browser DevTools** (F12)

2. **Go to Application tab** (Chrome/Edge) or Storage tab (Firefox)

3. **Find IndexedDB in the sidebar**

4. **Locate "VineVoiceExplorer" database**

5. **Right-click → Delete database**

6. **Or use AVE Settings:**
   - Open AVE Settings (⚙️)
   - Scroll to "Database Management"
   - Click "Delete Database"
   - Confirm deletion

## Troubleshooting

### Script Not Loading

**Problem:** Amazon Vine page looks normal, no AVE features

**Solutions:**
1. **Check Tampermonkey is enabled:**
   - Click Tampermonkey icon
   - Should show enabled scripts
   - Toggle might be off

2. **Check script is enabled:**
   - Open Tampermonkey Dashboard
   - Find "Amazon Vine Explorer"
   - Should have green checkmark
   - If not, click to enable

3. **Verify page match:**
   - Script runs on amazon.com, amazon.de, amazon.co.uk
   - Must be on a Vine page (/vine/ in URL)

4. **Check browser console:**
   - Press F12
   - Go to Console tab
   - Look for errors (red text)
   - Report errors if found

### Installation Fails

**Problem:** Can't install script from URL

**Solutions:**
1. **Try manual installation** (Method 2 above)

2. **Check internet connection**

3. **Disable ad blockers temporarily:**
   - Some ad blockers interfere with userscript installation

4. **Try different browser**

5. **Clear browser cache:**
   - May help with corrupted downloads

### Script Errors After Installation

**Problem:** Script loads but features don't work

**Solutions:**
1. **Update to latest version:**
   - Uninstall current version
   - Reinstall from repository

2. **Clear database:**
   - Delete IndexedDB as described above
   - Refresh page to rebuild

3. **Check browser compatibility:**
   - Update browser to latest version
   - Some features require modern JavaScript

4. **Disable conflicting extensions:**
   - Other Vine extensions may conflict
   - Try disabling them one by one

### Permission Errors

**Problem:** Browser shows permission warnings

**Solutions:**
1. **Tampermonkey needs permissions:**
   - Access to Amazon websites (normal)
   - Local storage access (normal)
   - Notification permission (optional)

2. **Grant required permissions:**
   - Browser will prompt when needed
   - Settings → Site settings → Permissions

3. **For notifications:**
   - Must grant notification permission
   - Browser prompts first time
   - Can revoke/grant in browser settings

### Update Not Working

**Problem:** Script doesn't update to latest version

**Solutions:**
1. **Check update URL:**
   - Edit script in Tampermonkey
   - Verify `@updateURL` is correct
   - Should point to repository

2. **Manually trigger update:**
   - Tampermonkey Dashboard
   - Click check for updates button

3. **Reinstall script:**
   - Uninstall old version
   - Install fresh from repository

4. **Check Tampermonkey settings:**
   - Update check should be enabled
   - Check interval should be set

## Getting Help

If you encounter issues:

1. **Check the User Guide:**
   - See [USER_GUIDE.md](USER_GUIDE.md)
   - Common questions answered

2. **Browser Console:**
   - Press F12 → Console tab
   - Look for error messages
   - Include in bug reports

3. **GitHub Issues:**
   - Visit: [AmazonVineExplorer/issues](https://github.com/matziq/AmazonVineExplorer/issues)
   - Search existing issues
   - Create new issue if needed

4. **Provide details in reports:**
   - Browser name and version
   - Tampermonkey version
   - AVE script version
   - Console errors
   - Steps to reproduce

## Advanced: Development Installation

For developers contributing to the project:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/matziq/AmazonVineExplorer.git
   ```

2. **Use local development script:**
   - Open `VineExplorerLocalDevelopment.user.js`
   - Update file:// paths to your local directory
   - Install in Tampermonkey

3. **Edit local files:**
   - Changes reflect after page refresh
   - No need to reinstall

4. **See [DEVELOPER_GUIDE.md](DEVELOPER_GUIDE.md)** for details

## Next Steps

After installation:
- Read the [USER_GUIDE.md](USER_GUIDE.md) for feature tutorials
- Configure settings (⚙️ button)
- Grant notification permission if desired
- Visit Amazon Vine and start using AVE!

Enjoy your enhanced Amazon Vine experience! 🎉
