# Sortable.js - Drag-and-Drop JavaScript Library

Sortable.js is a JavaScript library for reorderable drag-and-drop lists on modern browsers and touch devices. No jQuery required. Supports Meteor, AngularJS, React, Polymer, Vue, Knockout and any CSS library.

**Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.**

## Working Effectively

Bootstrap, build, and test the repository:
- `npm install` -- takes ~40 seconds. NEVER CANCEL. Set timeout to 90+ seconds.
- `npm run build` -- takes ~5 seconds. NEVER CANCEL. Set timeout to 30+ seconds.
- `npm run test` -- takes ~30-40 seconds. NEVER CANCEL. Set timeout to 90+ seconds.

Build individual targets:
- `npm run build:es` -- Build ES modules only (~2 seconds)
- `npm run build:umd` -- Build UMD module only (~2 seconds) 
- `npm run minify` -- Minify the built files (~1 second)

Run the demo application:
- Start local server: `python3 -m http.server 8080`
- Navigate browser to `http://localhost:8080`
- Test drag-and-drop functionality manually by dragging list items

Testing:
- `npm run test` -- Runs main TestCafe tests in Chrome headless (~40 seconds)
- `npm run test:compat` -- Compatibility tests using SauceLabs (requires external access, will fail in sandboxed environments)

## Validation

**CRITICAL**: Always manually validate drag-and-drop functionality after making changes:
1. Start the demo server: `python3 -m http.server 8080`
2. Open browser to `http://localhost:8080`
3. Test basic drag-and-drop in the "Simple list example" section
4. Drag Item 3 above Item 1 to verify reordering works
5. Test shared lists by dragging between left and right lists
6. Verify cloning works in the "Cloning" section
7. Test handle-based dragging in the "Handle" section

**Manual Testing Scenarios**:
- Simple reordering: Drag items within a single list
- Cross-list dragging: Move items between different lists  
- Cloning: Verify items are copied, not moved, when cloning is enabled
- Handle dragging: Verify dragging only works when grabbing the handle icon
- Filter testing: Verify filtered items cannot be dragged
- Grid layout: Test drag-and-drop in the grid example
- Nested sortables: Test complex nested drag-and-drop scenarios

The build process uses Rollup + Babel and generates multiple module formats.
- Never commit build artifacts in pull requests - they are generated during release

## Repository Structure

### Key Directories
- `src/` -- Source TypeScript/JavaScript files
  - `Sortable.js` -- Main library file
  - `Animation.js` -- Animation system
  - `utils.js` -- Utility functions
  - `PluginManager.js` -- Plugin system
- `plugins/` -- Plugin implementations
  - `AutoScroll/` -- Auto-scrolling during drag
  - `MultiDrag/` -- Multiple item selection and dragging
  - `OnSpill/` -- Handle drag outside sortable areas
  - `Swap/` -- Item swapping instead of sorting
- `scripts/` -- Build and test scripts
- `tests/` -- TestCafe browser tests
- `modular/` -- Built ES modules (generated)
- `entry/` -- Entry point files for different builds

### Build Outputs  
- `Sortable.js` -- UMD build (generated)
- `Sortable.min.js` -- Minified UMD build (generated)
- `modular/sortable.esm.js` -- ES module with default plugins
- `modular/sortable.core.esm.js` -- ES module core only
- `modular/sortable.complete.esm.js` -- ES module with all plugins

### Configuration Files
- `package.json` -- NPM configuration and scripts
- `babel.config.js` -- Babel transpilation config
- `.jshintrc` -- JSHint linting rules
- `.testcaferc.json` -- TestCafe test configuration
- `.circleci/config.yml` -- CircleCI build pipeline

## Common Tasks

Always run build validation steps:
1. `npm install` (if dependencies changed)
2. `npm run build` 
3. `npm run test`
4. Manual demo testing as described above

### Making Code Changes
- Edit source files in `src/` directory
- Plugin changes go in respective `plugins/` subdirectories  
- Always rebuild after changes: `npm run build`
- Always test: `npm run test`
- Always manually validate in demo: `python3 -m http.server 8080`

### Development Workflow
- Watch builds during development:
  - `npm run build:es:watch` -- Watch ES module builds
  - `npm run build:umd:watch` -- Watch UMD builds
- Test individual components using the HTML files in `tests/` directory

### CI/CD Information
- Uses CircleCI (not GitHub Actions)
- Builds on Node.js 10.16 with browsers
- Runs compatibility tests on SauceLabs (external service)
- Configuration in `.circleci/config.yml`

## Timing Expectations
- `npm install`: ~40 seconds. NEVER CANCEL. Set timeout to 90+ seconds.
- `npm run build`: ~5 seconds. NEVER CANCEL. Set timeout to 30+ seconds.
- `npm run test`: ~30-40 seconds. NEVER CANCEL. Set timeout to 90+ seconds.
- `npm run build:es`: ~2 seconds
- `npm run build:umd`: ~2 seconds  
- `npm run minify`: ~1 second
- Demo server startup: ~1 second

## Known Issues and Workarounds
- Compatibility tests (`npm run test:compat`) require SauceLabs access and will fail in sandboxed environments
- Build shows "Browserslist: caniuse-lite is outdated" warnings - these are non-fatal
- Build shows circular dependency warnings - these are expected and non-fatal
- Some npm packages show deprecation warnings during install - these don't affect functionality

## Quick Reference Commands

```bash
# Full development setup
npm install
npm run build
npm run test

# Start demo server  
python3 -m http.server 8080

# Watch builds during development
npm run build:es:watch
# OR
npm run build:umd:watch

# Individual build steps
npm run build:es      # ES modules
npm run build:umd     # UMD module  
npm run minify        # Minify outputs

# Testing
npm run test          # Main tests (~40s)
npm run test:compat   # Compatibility tests (requires SauceLabs)
```