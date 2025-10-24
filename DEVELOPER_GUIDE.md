# Amazon Vine Explorer - Developer Guide

## Table of Contents
1. [Architecture Overview](#architecture-overview)
2. [Project Structure](#project-structure)
3. [Core Components](#core-components)
4. [Development Setup](#development-setup)
5. [Building & Testing](#building--testing)
6. [Contributing](#contributing)
7. [Code Style](#code-style)

## Architecture Overview

Amazon Vine Explorer (AVE) is a Tampermonkey/Greasemonkey userscript that enhances the Amazon Vine website experience. It uses a modular architecture with several key components:

### Technology Stack
- **JavaScript** (ES6+)
- **IndexedDB** for local data persistence
- **Tampermonkey/Greasemonkey API** for browser integration
- **Amazon Vine API** for product data
- **Browser Notifications API** for desktop alerts

### Design Principles
1. **Local-first**: All data stored in browser IndexedDB
2. **Non-intrusive**: Enhances existing Vine UI without breaking it
3. **Compliant**: No automated ordering or unfair advantages
4. **Performance**: Optimized database queries and DOM manipulation
5. **Privacy**: No external data transmission except to Amazon

## Project Structure

```
AmazonVineExplorer/
├── VineExplorer.user.js          # Main userscript file
├── globals.js                     # Global constants and settings
├── class_db_handler.js           # Database handler class
├── class_product.js              # Product data model
├── DataBaseMigrator.user.js      # Database migration tool
├── FileSaver.js                  # External: File download library
├── fetchfix.js                   # External: Fetch API fixes
├── README.md                     # Project readme
├── USER_GUIDE.md                 # End-user documentation
├── DEVELOPER_GUIDE.md            # This file
├── INSTALLATION.md               # Installation instructions
└── LICENSE                       # MIT License
```

### File Descriptions

#### VineExplorer.user.js
Main script file containing:
- Userscript metadata header
- Page detection and initialization
- UI rendering and event handlers
- Background scan logic
- Notification system
- Settings management

#### globals.js
Global configuration including:
- Constants (database names, versions)
- Settings definitions schema
- Default settings values
- CSS style definitions
- Helper functions
- Event handler class

#### class_db_handler.js
Database abstraction layer:
- IndexedDB initialization
- CRUD operations (Promise-based)
- Database migration logic
- Index management
- Bulk operations

#### class_product.js
Product data model:
- Product properties definition
- Data normalization
- Validation helpers

#### DataBaseMigrator.user.js
Standalone migration tool for converting legacy VineViewer databases to AVE format.

## Core Components

### 1. Database Layer (DB_HANDLER)

The database handler provides Promise-based access to IndexedDB.

**Key Methods:**
```javascript
// Initialize database
database.init(callback)

// Add product
await database.add(productObject)

// Get product by ID
const product = await database.get(productId)

// Update product
await database.update(productObject)

// Get all products
const products = await database.getAll()

// Get new products
const newProducts = await database.getNewEntries()

// Get favorites
const favorites = await database.getFavorites()

// Search products
const results = await database.search(query)
```

**Database Schema:**
```javascript
{
  id: string,                    // Unique identifier
  link: string,                  // Product link
  description_full: string,      // Full description
  description_short: string,     // Short description
  data_recommendation_id: string,
  data_recommendation_type: string,
  data_img_url: string,
  data_img_alt: string,
  data_asin: string,
  isFav: boolean,               // Favorite flag
  isNew: boolean,               // New/unread flag
  gotRemoved: boolean,          // Removed from Vine
  ts_firstSeen: number,         // Unix timestamp
  ts_lastSeen: number,          // Unix timestamp
  notSeenCounter: number,       // Increments when not seen
  order_success: boolean,
  generated_short: boolean,
  queue: string                 // Vine queue type
}
```

**Indexes:**
- Primary key: `id`
- Index: `isNew`
- Index: `isFav`

### 2. Settings System

Settings are managed through `SETTINGS_USERCONFIG_DEFINES` in globals.js.

**Settings Schema:**
```javascript
{
  key: string,           // Setting identifier
  type: string,          // 'bool', 'number', 'color', 'keywords', 'title'
  name: string,          // Display name
  description: string,   // Help text
  min: number,          // For type 'number'
  max: number,          // For type 'number'
  inputPlaceholder: string  // For type 'keywords'
}
```

**Settings Storage:**
- Saved to `GM_setValue` (Tampermonkey storage)
- Retrieved with `GM_getValue`
- Persists across browser sessions
- Syncs across Tampermonkey instances

### 3. Background Scanner

Automatically scans Vine queues for new products.

**Flow:**
1. Detect master/slave session
2. Only master session runs scan
3. Loop through Vine queues (encore, last_chance, potluck)
4. Fetch product tiles from each page
5. Parse and store in database
6. Fetch product details via API
7. Trigger notifications for new products
8. Apply configurable delays between requests

**Key Functions:**
```javascript
initBackgroundScan()           // Start background scan
backgroundAutoScan()           // Main scan loop
autoScanQueuePage(queue, page) // Scan specific queue page
parseTileData(tile)           // Extract data from product tile
```

### 4. Notification System

Desktop notifications with keyword highlighting.

**Key Functions:**
```javascript
desktopNotification(title, message, image, requireInteraction, onClick)
updateNewProductsBtn()  // Checks for new products and triggers notifications
```

**Notification Logic:**
1. Check if notifications enabled
2. Check keyword matches (immediate notification)
3. Check notification delay timer
4. Create browser notification
5. Update last notification timestamp

### 5. UI Rendering

Dynamic UI generation for custom Vine pages.

**Key Functions:**
```javascript
createProductSite(products, pageTitle)  // Main product grid
createTileFromProduct(product)          // Individual product tile
createNavButton(id, text, ...)          // Navigation buttons
createSettingsPage()                     // Settings UI
addLeftSideButtons()                    // Left navigation panel
```

### 6. Share System

Generate shareable Vine product links.

**Key Functions:**
```javascript
shareEventHandlerClick(event, data)  // Handle share button click
createSharePopup(data)                // Generate share UI
```

**Share URL Format:**
```
https://www.amazon.{domain}/vine/vine-items?vine-data={encodedData}
```

## Development Setup

### Prerequisites
- Modern web browser (Chrome, Firefox, Edge)
- Tampermonkey extension installed
- Text editor or IDE (VS Code recommended)
- Git for version control

### Local Development

#### Method 1: Direct File Editing
1. Clone the repository
2. Open `VineExplorer.user.js` in Tampermonkey dashboard
3. Edit and save
4. Refresh Amazon Vine page to test

#### Method 2: Local Development Script
Use `VineExplorerLocalDevelopment.user.js`:
1. Update `@require` paths to local file:// URLs
2. Install in Tampermonkey
3. Edit local files
4. Reload page to test changes

**Example @require for local dev:**
```javascript
// @require file:///D:/AmazonVineExplorer/globals.js
// @require file:///D:/AmazonVineExplorer/class_db_handler.js
// @require file:///D:/AmazonVineExplorer/class_product.js
```

### Debugging

**Console Logging:**
Set `DebugLevel` in settings to enable verbose logging:
- 0 = Errors only
- 1-5 = Normal debugging
- 10+ = Verbose debugging
- 100+ = Very verbose (performance impact)

**Browser DevTools:**
```javascript
// Access AVE internals from console
unsafeWindow.ave.config     // Current settings
unsafeWindow.ave.classes    // Class instances
unsafeWindow.ave.event      // Event handler
```

**Database Inspection:**
1. Open DevTools (F12)
2. Go to Application → Storage → IndexedDB
3. Expand `VineVoiceExplorer` database
4. View object stores and data

## Building & Testing

### Code Quality Checks

Before committing:
1. Test on all supported Amazon domains (.com, .de, .co.uk)
2. Test with fresh database (delete existing)
3. Test with populated database
4. Test background scan
5. Test notifications
6. Test all settings changes
7. Check browser console for errors

### Version Numbering

Format: `a.b.c[.d]`

- **a** = Major version (breaking changes)
- **b** = Minor version (new features)
- **c** = Patch version (bug fixes)
- **d** = Micro version (small hotfixes, optional)

Update version in:
1. Userscript header `@version`
2. `AVE_VERSION` constant in globals.js
3. Changelog in README.md

### Testing Checklist

- [ ] Fresh install works
- [ ] Database migration works
- [ ] All navigation buttons functional
- [ ] Search works with multiple keywords
- [ ] Favorites add/remove works
- [ ] Mark as seen functions work
- [ ] Background scan detects new products
- [ ] Notifications appear correctly
- [ ] Settings save and load
- [ ] Export/import database works
- [ ] Dark mode works
- [ ] Share links work
- [ ] No console errors
- [ ] Performance is acceptable

## Contributing

### Contribution Guidelines

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes**
   - Follow code style guidelines
   - Add comments for complex logic
   - Update documentation if needed
4. **Test thoroughly**
5. **Commit with clear messages**
   ```bash
   git commit -m "Add feature: description of feature"
   ```
6. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```
7. **Create a Pull Request**
   - Describe changes clearly
   - Reference any related issues
   - Include screenshots if UI changes

### Code Review Process

PRs will be reviewed for:
- Code quality and style
- Functionality and correctness
- Performance impact
- Documentation completeness
- Test coverage
- Compliance with Vine terms of service

## Code Style

### JavaScript Style

**General:**
- Use camelCase for variables and functions
- Use PascalCase for classes
- Use SCREAMING_SNAKE_CASE for constants
- Prefer `const` over `let`, avoid `var`
- Use template literals for string interpolation
- Add semicolons

**Naming Conventions:**
```javascript
// Variables
const productCount = 10;
let currentPage = 1;

// Functions
function parseTileData(tile) { }
async function fetchProductDetails() { }

// Classes
class DB_HANDLER { }
class Product { }

// Constants
const DATABASE_NAME = 'VineVoiceExplorer';
const MAX_RETRY_ATTEMPTS = 3;

// Private variables (convention)
const _privateVar = 'internal';
```

**Functions:**
```javascript
// Prefer arrow functions for callbacks
products.map(p => p.id);

// Use async/await over promises
async function getData() {
  const result = await database.get(id);
  return result;
}

// Add JSDoc comments for public functions
/**
 * Send a Desktop Notification
 * @param {string} title - Notification title
 * @param {string} message - Notification body
 * @param {string} image - Optional image URL
 * @param {boolean} requireInteraction - Keep notification until clicked
 * @param {function} onClick - Callback for notification click
 */
function desktopNotification(title, message, image = null, requireInteraction = null, onClick = () => {}) {
  // Implementation
}
```

**Comments:**
```javascript
// Single-line comments for brief explanations

/*
 * Multi-line comments for longer descriptions
 * or complex logic explanations
 */

/**
 * JSDoc comments for functions, classes, and important variables
 * @param {type} name - description
 * @returns {type} description
 */
```

### HTML/CSS Style

**CSS:**
- Use kebab-case for class names
- Prefix AVE-specific classes with `ave-`
- Group related styles together
- Comment style sections

```javascript
const css = `
  /* Navigation buttons */
  .ave-btn-container { }
  .ave-btn { }
  
  /* Product tiles */
  .ave-tile { }
  .ave-tile-new { }
`;
```

### Database Operations

Always use try/catch with database operations:
```javascript
try {
  const product = await database.get(productId);
  if (product) {
    // Process product
  }
} catch (error) {
  console.error('Database error:', error);
}
```

### Performance Considerations

1. **Minimize DOM Queries**
   ```javascript
   // Bad
   for (let i = 0; i < 100; i++) {
     document.getElementById('container').appendChild(element);
   }
   
   // Good
   const container = document.getElementById('container');
   for (let i = 0; i < 100; i++) {
     container.appendChild(element);
   }
   ```

2. **Batch Database Operations**
   ```javascript
   // Use transactions for multiple operations
   const transaction = database._db.transaction(['storeName'], 'readwrite');
   // Perform multiple operations
   ```

3. **Debounce Expensive Operations**
   ```javascript
   let searchTimeout;
   searchInput.addEventListener('input', (e) => {
     clearTimeout(searchTimeout);
     searchTimeout = setTimeout(() => {
       performSearch(e.target.value);
     }, 300);
   });
   ```

## API Reference

### Tampermonkey APIs Used

```javascript
// Storage
GM_setValue(key, value)        // Store data
GM_getValue(key, defaultValue) // Retrieve data

// HTTP Requests
GM.xmlHttpRequest({
  method: 'GET',
  url: 'https://...',
  onload: (response) => { }
})

// Access unsafe window
unsafeWindow.addEventListener(...)
```

### Amazon Vine API Endpoints

The script interacts with these Amazon endpoints:

```javascript
// Product details
`https://www.amazon.${domain}/vine/api/recommendations/${recId}/item/${asin}`

// Product tiles (internal pages)
`https://www.amazon.${domain}/vine/vine-items?queue=${queue}&page=${page}`
```

## Troubleshooting Development Issues

### Script not loading
- Check userscript metadata is correct
- Verify `@match` patterns
- Check browser console for errors

### Database errors
- Clear IndexedDB in DevTools
- Check database version number
- Verify migration logic

### Performance issues
- Profile with DevTools Performance tab
- Check for excessive DOM queries
- Monitor database operation times
- Reduce debug logging

### CSS not applying
- Check for CSS injection timing
- Verify selectors are correct
- Look for CSS conflicts with Amazon's styles

## Resources

- [Tampermonkey Documentation](https://www.tampermonkey.net/documentation.php)
- [IndexedDB API](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)
- [Notifications API](https://developer.mozilla.org/en-US/docs/Web/API/Notifications_API)
- [Greasemonkey API](https://wiki.greasespot.net/Greasemonkey_Manual:API)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
