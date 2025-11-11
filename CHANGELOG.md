# Changelog

All notable changes to this project will be documented in this file.

## [0.0.11] - 2025-11-11

### Fixed

- **Docker Build Errors**: Fixed critical Docker build issues (Issues #2, #3)
  - Moved `typescript` from `peerDependencies` to `devDependencies` to fix "tsc: not found" error
  - Changed Dockerfile to use `npm ci` instead of `npm install --ignore-scripts` for proper dependency installation
  - Fixed incorrect output paths in package.json:
    - Updated bin path from `dist/src/mcp/server.js` to `dist/mcp/server.js`
    - Updated files paths to match actual build output structure
    - Updated start and inspect scripts to use correct paths
  - Fixed Dockerfile CMD to use correct path `dist/mcp/server.js`
  - Fixed tsconfig.json to exclude config files from compilation

### Changed

- Docker builds now properly install TypeScript during build phase
- Build output structure correctly outputs to `dist/` instead of `dist/src/`

## [0.0.10] - Previous release

### Changes

- Previous changes...
