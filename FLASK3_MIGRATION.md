# Flask 3.x Migration Summary

This document summarizes the changes made to update Flask-Mako for compatibility with Flask 3.x.

## Changes Made

### 1. Removed Unused Import
- **File**: `flask_mako.py`
- **Change**: Removed unused import of `locked_cached_property` from `flask.helpers`
- **Reason**: `locked_cached_property` was removed in Flask 3.x and was not actually used in the code

### 2. Updated Context Stack Usage
- **File**: `flask_mako.py`
- **Change**: Replaced `_app_ctx_stack` and `_request_ctx_stack` with `current_app`
- **Reason**: Context stacks were removed in Flask 3.x; `current_app` is the recommended approach

### 3. Updated Werkzeug Debug Imports
- **File**: `flask_mako.py`
- **Change**: 
  - `Traceback` → `DebugTraceback`
  - `Frame` → `DebugFrameSummary`
  - Added custom `Line` class (no longer available in Werkzeug)
- **Reason**: Werkzeug debug classes were renamed/removed in newer versions

### 4. Updated MakoFrame Class
- **File**: `flask_mako.py`
- **Change**: Updated constructor to work with new `DebugFrameSummary` signature
- **Reason**: `DebugFrameSummary` has a different constructor than the old `Frame` class

### 5. Fixed Signal Sender Issue
- **File**: `flask_mako.py`
- **Change**: Use `current_app._get_current_object()` instead of `current_app` for signal sending
- **Reason**: `current_app` is a proxy object; signals need the actual app instance for proper sender matching

### 6. Updated Test Compatibility
- **File**: `tests/test_mako.py`
- **Change**: Removed `flask.signals_available` check
- **Reason**: Signals are always available in Flask 3.x

### 7. Updated Package Metadata
- **File**: `setup.py`
- **Changes**:
  - Version bumped to `0.6.0`
  - Flask dependency updated to `>=2.0,<4.0`
- **Reason**: Reflect Flask 3.x support and version the release appropriately

## Compatibility

- **Flask**: 2.0+ through 3.x
- **Python**: 3.8+ (required for some of the compatibility features)
- **Werkzeug**: Compatible with versions bundled with Flask 2.0+

## Testing

All existing tests pass with Flask 3.x. The test suite includes:
- Basic template rendering
- Template context handling
- Signal firing
- Multiple app support
- Error handling
- Babel integration (if available)

## Breaking Changes

None. This update maintains backward compatibility while adding Flask 3.x support.
