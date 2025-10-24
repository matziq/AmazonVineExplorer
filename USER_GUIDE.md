# Amazon Vine Explorer - User Guide

## Table of Contents
1. [Getting Started](#getting-started)
2. [Interface Overview](#interface-overview)
3. [Features](#features)
4. [Settings](#settings)
5. [Tips & Tricks](#tips--tricks)
6. [Troubleshooting](#troubleshooting)

## Getting Started

### First Launch
After installing Amazon Vine Explorer, visit any Amazon Vine page. The script will:
1. Initialize a local database (IndexedDB)
2. Add new navigation buttons to the left side
3. Add a settings button (⚙️) to the navigation
4. Begin cataloging products you view

### Understanding the Display
Products are displayed with color-coded borders:
- **Green border with light background** - New products you haven't seen
- **Yellow border** - Products you've marked as favorites (⭐)
- **Red border** - Products that have been removed from Vine
- **Blue border** - Standard products you've already seen

## Interface Overview

### Left Navigation Panel

#### 🆕 New Products Button
- Shows count of new/unread products in a badge
- Click to view all products marked as "new"
- Badge updates automatically as you browse

#### ⭐ Favorites Button
- View products you've starred as favorites
- Click the star icon on any product tile to add to favorites
- Yellow star = favorited, white star = not favorited

#### 📦 All Products Button
- Infinite scroll view of entire product catalog
- Loads products from your local database
- Faster than querying Amazon repeatedly

#### ✅ Mark Current Page as Seen
- Marks all products on the current page as "seen"
- Removes "new" status from these products

#### ✅ Mark All as Seen
- Marks ALL products in database as "seen"
- Useful after reviewing the entire catalog

#### ⬆️ Back to Top
- Quick scroll to top of page
- Available on all Vine pages

### Search Bar
- Located at the top of the navigation
- Search your local product database
- Supports multiple keywords (space-separated)
- Minimum 2 characters required
- Case-insensitive search

### Settings Button (⚙️)
- Opens the AVE Settings panel
- Customize all script behaviors
- Changes save automatically

## Features

### Desktop Notifications

Get browser notifications when new products arrive!

**Setup:**
1. Click Settings (⚙️)
2. Enable "Enable Desktop Notifications"
3. Grant browser notification permission when prompted
4. Configure notification delay (minimum seconds between notifications)

**Keyword Highlighting:**
- Add keywords in Settings → "Desktop Notification Highlight Keywords"
- Type keyword and press ENTER to add
- Products matching keywords trigger immediate notifications
- Bypasses the normal notification delay

### Background Scanning

Automatically monitors Amazon Vine for new products while you browse.

**How it works:**
1. Runs in the background on Vine pages
2. Checks all Vine queues periodically
3. Updates your local database
4. Triggers notifications for new products

**Configuration:**
- **Background Scan Per Page Min Delay** - Minimum time between page loads (milliseconds)
- **Background Scan Randomness** - Random delay added per page (helps avoid detection)
- Higher delays = more "human-like" behavior

**Note:** Only one browser tab should run background scan at a time. AVE automatically detects "master" vs "slave" sessions.

### Dark Mode

Toggle between light and dark themes.

**Enable:**
1. Settings → Enable Dark Mode
2. Customize dark mode colors:
   - Background Color
   - Text Color

### Product Sharing

Generate shareable links that open directly in Vine product details.

**How to share:**
1. Click "More details" on any product
2. Look for the share icon/button
3. Click to copy link to clipboard
4. Share the link with other Vine Voices

**Supported queues:**
- Potluck (FSE)
- Available for all
- Additional items

### Favorites System

Mark important products for easy access later.

**Add to favorites:**
- Click the ⭐ star icon on any product tile
- Star turns yellow when favorited

**View favorites:**
- Click the ⭐ Favorites button in left navigation
- Shows only products you've starred
- Favorites are preserved even if product is removed from Vine

### Data Management

#### Export Database
1. Settings → Export Database
2. Downloads JSON file with all your data
3. Keep as backup or transfer to another browser

#### Import Database
1. Settings → Import Database
2. Paste JSON data or load from file
3. Merges with existing database (doesn't overwrite)

#### Delete Database
1. Settings → Delete Database
2. Confirms before deletion
3. Removes all local data
4. Fresh start - script will rebuild database

## Settings

### Display Settings

**Enable Top Logo Change**
- Replaces Amazon Vine logo with AVE branding
- Shows database activity indicators

**Hide Amazon Navbar**
- Removes the standard Amazon navigation bar
- Provides more screen space for products

**Hide Amazon Categories**
- Hides the category filter bar
- Cleaner product view

**Enable Infinite Scroll Live Query**
- When enabled: queries Amazon directly (slower, always current)
- When disabled: loads from local database (faster)

### Button Colors

Customize colors for all navigation buttons:
- New Products button
- Favorites button
- Mark as Seen buttons
- Back to Top button
- All Products button

Click the color picker to choose custom colors.

### Star Colors

- **Default Star Color** - Unfavorited products
- **Checked Star Color** - Favorited products

### Product Tile Styles

Advanced: Customize CSS for product tile borders and backgrounds.

Settings for:
- New products
- Saved products
- Favorited products
- Removed products
- Default products

## Tips & Tricks

### Efficient Workflow
1. Enable background scan to auto-catalog products
2. Set up notification keywords for items you want
3. Periodically click "All Products" to review entire catalog
4. Use "Mark All as Seen" after reviewing to reset new counter
5. Star interesting products for later review

### Keyword Strategy
- Add brand names you trust
- Add product categories you prefer
- Add specific item types (e.g., "wireless", "cookbook")
- Keep list focused - too many keywords = too many notifications

### Performance Tips
- Increase background scan delays if experiencing issues
- Use "All Products" (database mode) instead of live queries
- Periodically export/backup your database
- Delete database if it becomes corrupted or too large

### Multi-Tab Usage
- Only one tab should be the "master" session
- Master session runs background scan
- Look at bottom-left branding:
  - "M" indicator = Master session
  - "S" indicator = Slave session

## Troubleshooting

### Products not updating
- Check if background scan is enabled
- Verify you're on the master session
- Manually refresh the Vine page
- Check browser console for errors (F12)

### Notifications not working
- Ensure notifications are enabled in Settings
- Grant browser notification permission
- Check notification delay setting
- Verify keywords are entered correctly

### Database issues
- Export database as backup
- Try deleting and rebuilding database
- Clear browser cache
- Reinstall the script

### Script not loading
- Verify Tampermonkey is enabled
- Check that script is enabled in Tampermonkey dashboard
- Update to latest version
- Check browser console for errors

### Performance problems
- Increase background scan delays
- Disable infinite scroll live query
- Reduce number of notification keywords
- Close extra browser tabs

## Support

For issues, feature requests, or questions:
- GitHub Issues: [Amazon-Vine-Explorer/AmazonVineExplorer](https://github.com/Amazon-Vine-Explorer/AmazonVineExplorer/issues)
- Check existing issues before creating new ones
- Provide browser version and script version in bug reports

## Privacy & Data

All data is stored locally in your browser (IndexedDB). Nothing is sent to external servers except:
- Standard Amazon Vine API calls (same as normal Vine usage)
- Script update checks (if configured in Tampermonkey)

Your product catalog, favorites, and settings never leave your browser.
