# Changelog

## [1.0.5] 2026-06-13

### Fixed
- Fixed false-positive `invalid-type-keyword` on UDT array types such as `OrderBlock[]` and `FVG[]`.
- Fixed false-positive `same-row-statements` for valid comma-separated variable declarations.
- Improved recognition of Pine Script v6 built-in types including `footprint`.
- Fixed false-positive `unknown-function-reference` for binary operator `and`.

### Added
- New diagnostic check for `return` statements used outside function contexts.

## [1.0.3] 2026-06-13

### Fixed
- Reduced false-positive diagnostics in valid Pine Script files, including loop ranges and typed field declarations.
- Improved accuracy on real-world scripts so valid code is less likely to be marked as broken.

## [1.0.2] 2026-06-12

### Fixed
- Significantly reduced false-positive errors on built-in Pine Script v6 indicators and strategies, so valid scripts are no longer marked as broken.

## [1.0.1] 2026-06-12

### Fixed
- Reduced false syntax and parsing errors in multiline and complex expressions.

### Improved
- Updated Marketplace description and keywords so the extension is easier to discover and feature coverage is clearer.

## [1.0.0] 2026-06-11

### Added
- IntelliSense now covers many more Pine Script v6 built-in functions, with richer signatures, hover docs, and completions.
- Added diagnostics for unsupported bitwise operators so scripts fail less often at publish/runtime time.

### Fixed
- Restored missing completions and hover documentation for built-in Pine Script function groups.

## [0.9.9] 2026-06-10

### Fixed
- Reduced multiple false-positive diagnostics in valid Pine scripts.
- Improved detection of real syntax issues in copied or malformed code.
- Improved handling of non-standard file text formatting and special characters.
- Added validation for unresolved merge conflict markers.

## [0.9.8] 2026-06-10

### Fixed
- Added clearer diagnostics for invalid tuple assignment patterns.

## [0.9.7] 2026-06-10

### Fixed
- Version directive detection is now more tolerant and avoids false warnings.

## [0.9.6] 2026-06-10

### Fixed
- Reduced false-positive diagnostics in valid scripts, especially in advanced function and declaration patterns.
- Added diagnostics for common script declaration typos.
- Added diagnostics for invalid alert message value types.

## [0.9.4] 2026-06-09

### Added
- Pine Script files now appear in **File → New File...** - pick **Pine Script Indicator** or **Pine Script Strategy** directly from VS Code's built-in new file menu
- New keyboard shortcuts: `Cmd+K, Cmd+I` (Indicator) and `Cmd+K, Cmd+S` (Strategy) on macOS; `Ctrl+K, Ctrl+I` / `Ctrl+K, Ctrl+S` on Windows and Linux

### Fixed
- Reduced false errors on typed declarations and mixed-indentation files.
- "Open external website" dialog no longer appears when clicking CodeLens entries
- Removed Library template (not supported in this release)

## [0.9.3] 2026-06-09

### Fixed
- Syntax error detection was not working - standalone invalid identifiers and other structural errors were not reported. Now all syntax checks work correctly.

## [0.9.2] 2026-06-09

### Fixed
- Fixed false trailing-comma diagnostics in valid function calls.
- Extension stability: the extension host no longer crashes when opening complex or mixed-indentation Pine Script files

## [0.9.1] 2026-06-09

### Fixed
- Fixed false “used before declaration” diagnostics for property access expressions.
- Fixed false bare-number diagnostics inside valid string content.

## [0.9.0] 2026-06-09

### Added
- IntelliSense now includes your own functions, variables, types and parameters - autocomplete works across the entire file, not just built-ins
- Function parameters appear in completions inside the function body
- Hover tooltips now show documentation for user-defined symbols

### Improved
- Diagnostics now catch more real-world Pine Script mistakes while keeping fewer false positives.

## [0.8.9] 2026-06-08

### Added
- Added diagnostics for missing operators around numeric values.
- Added diagnostics for invalid standalone statements at global scope.

### Improved
- Reliability and quality improvements.

## [0.8.8] 2026-06-07

### Added
- Added diagnostics for unsupported non-ASCII symbols in code.
- Added diagnostics for scope-related usage mistakes in scripts.

### Improved
- Reliability and quality improvements.

## [0.8.7] 2026-06-07

### Added
- **User-defined symbol support** - IntelliSense now understands your own functions, variables and types
  - Completion, hover and signature help work for user-defined functions (with full parameter list)
  - Hover shows fields for User-Defined Types (`type MySignal ...`)
  - UDT field and method completion after `myVar.` when the type is known
  - Completion shows user variables with inferred or declared type
- **3 new diagnostics**
  - Better scope validation
  - Better script-type validation
  - Better input placement validation

## [0.8.6] 2026-06-06

### Improved
- Diagnostics are smarter about multiline expressions and produce fewer false warnings.
- Diagnostics no longer flag function parameters as undeclared variables
- Diagnostics correctly detect duplicate `var` declarations in the same scope

## [0.8.5] 2026-06-06

### Added
- Diagnostics now warn when a variable is used before it is declared
- Diagnostics now detect common logical-expression continuation mistakes.

### Improved
- Reliability and stability improvements.

## [0.8.4] 2026-06-06

### Fixed
- Keyboard shortcuts `Cmd+Option+I` and `Cmd+Option+S` now work from any file, not only when a `.pine` file is active

### Improved
- Marketplace description updated with correct keyboard shortcut labels for macOS

## [0.8.3] 2026-06-06

### Improved
- Marketplace page updated with clearer structure and better descriptions for all features

## [0.8.2] 2026-06-06

### Improved
- Updated `.pine` file icon with a new design that looks sharper in the VS Code file explorer
- Diagnostics no longer flag commented-out lines as errors - only real code is analyzed

## [0.8.1] 2026-06-06

### Improved
- Marketplace page updated with clearer description, better structure and improved readability
- Improved release stability after marketplace migration

## [0.8.0] 2026-06-06

### Improved
- Syntax highlighting now correctly recognizes generic type angle brackets such as `array<float>` and `matrix<int>`
- Bracket and punctuation characters are styled consistently in both Dark and Light themes
- Bracket pair colorization is disabled by default to avoid conflicts with Pine Script syntax colors

## [0.7.0] 2026-06-05

### Changed
- Faster code intelligence and navigation performance.
- Stability and correctness improvements.

## [0.6.0] 2026-06-05

### Added
- **Find All References** (Shift+F12) finds all usages of any user-defined symbol
- **Clickable Links** TradingView URLs in comments are now hyperlinks
- **Color Picker** inline color picker for `color.rgb()` and all `color.*` constants
- **Format Document** normalizes indentation, trims trailing whitespace, collapses excess blank lines
- **Getting Started Walkthrough** 4-step onboarding in the VS Code Help tab
- Added new settings to control references, color tools, and formatting behavior.

## [0.5.0] 2026-06-05

### Added
- **Rename Symbol** (F2) renames any user-defined symbol across the file
- **Smart Folding** improves folding for script structures and long declarations.
- **Code Lens** shows usage count above every user-defined function
- **Pine Script Explorer** Activity Bar sidebar to browse all built-in namespaces and insert symbols

## [0.4.0] 2026-06-05

### Added
- **Real-time Diagnostics** for common Pine Script mistakes.
- **Go to Definition** (F12) jumps to user-defined symbols and opens TradingView docs for built-ins
- **Document Highlight** highlights all occurrences of the symbol under cursor in real time
- **Status Bar** shows `Pine Script v6` or a warning for every active `.pine` file
- **Open on TradingView** button in the editor title bar
- Added new settings for diagnostics, hover links, and completion behavior.

## [0.3.0] 2026-06-04

### Changed
- Smaller extension download size
- Faster extension activation

## [0.2.0] 2026-06-04

### Added
- **Document Outline** shows functions, variables, UDTs and inputs in breadcrumbs and the Outline panel
- **Code Actions** quick fixes for common script setup and structure issues.
- **Semantic Highlighting** colors user-defined functions, variables, types and parameters distinctly
- **@pinescript Chat** AI assistant for explaining and scaffolding Pine scripts.

## [0.1.0] 2026-06-04

### Added
- Pine Script v6 language support for `.pine` files
- Syntax highlighting for keywords, namespaces, types, operators and annotations
- IntelliSense with 566+ functions, constants and variables from TradingView docs
- Hover tooltips with signatures, parameters, examples and doc links
- Signature help while typing function arguments
- 25+ code snippets for indicator/strategy/library scaffolds, TA functions and control flow
- New file templates: Indicator, Strategy, Library
- Pine Script Dark and Light color themes
- Custom `.pine` file icon in dark and light variants
