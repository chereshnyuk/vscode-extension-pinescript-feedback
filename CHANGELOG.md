# Changelog

## [1.0.1] 2026-06-12

### Fixed
- Improved parsing for multiline continuation patterns and comma-separated expressions used in Pine scripts, reducing false syntax/parse errors.

### Improved
- Updated Marketplace description and keywords so the extension is easier to discover and feature coverage is clearer.

## [1.0.0] 2026-06-11

### Added
- IntelliSense now covers 488 Pine Script v6 built-in functions (up from 299) — ta.*, math.*, strategy.*, request.*, str.* and more are fully indexed with signatures, hover docs, and completions
- New `bitwise-operator` diagnostic flags `<<`, `>>`, `&`, `|`, `^` operators that TradingView rejects (CE10005)

### Fixed
- Completions and hover docs were missing for all `ta.*`, `math.*`, `strategy.*`, `request.*`, and `str.*` functions — now correctly loaded from the reference documentation

## [0.9.9] 2026-06-10

### Fixed
- Removed false "bare number" errors on numbers inside multi-line string literals (e.g. `"...value is 0..."`)
- Removed false "bare number" errors after the `is` type-check keyword
- Removed false `request.security() in loop` errors — Pine Script v6 allows this
- Removed false "invalid-statement" for `void` return-type annotations on functions (`void myFunc() =>`)
- Removed false "invalid-statement" for `float`/`int`/`bool` array-type variants (`float[]`, `int[]`, etc.)
- Removed false "invalid-statement" when a grammar artifact identifier has any sibling on the same row (more robust check)
- Removed false "missing //@version=6" in files with `\r\r\n` line endings (increased version search range to 15 lines)
- Added `non-ascii-char` detection for non-breaking and other special Unicode spaces (U+00A0, U+2002, U+2003, U+2009, U+200B) that cause TradingView lexer errors
- Added `merge-conflict-marker` error for git conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) left in code
- Removed false "line-continuation" errors for `and`/`or` inside indented blocks
- Removed false "invalid-statement" for `plot(series = signal, ...)` — `series` is a qualifier keyword but the call is still valid

## [0.9.8] 2026-06-10

### Fixed
- Added detection of type annotations inside tuple destructuring brackets — `[float a, float b] = func()` is now flagged as a syntax error (TradingView rejects it; use `[a, b] = func()` instead)

## [0.9.7] 2026-06-10

### Fixed
- No longer reports "Missing //@version=6" when the file uses `// @version=6` (with a space after `//`) — TradingView accepts both forms

## [0.9.6] 2026-06-10

### Fixed
- Removed false errors on `varip` inside function bodies — Pine Script v6 supports this
- Removed false "invalid statement" errors on `float`/`int`/`color` typed declarations in comma-separated multi-variable lines
- Removed false "used before declaration" errors when a local variable inside a function shares its name with a global variable declared later in the file
- Removed false "line continuation" errors on indented continuation lines and files with non-standard `\r\r\n` line endings
- Added detection of misspelled script type declarations (e.g. `indicato3r()` now reported as an error)
- Added detection of `series string` passed to `alertcondition(message=...)` — TradingView requires a `const string` there

## [0.9.4] 2026-06-09

### Added
- Pine Script files now appear in **File → New File...** — pick **Pine Script Indicator** or **Pine Script Strategy** directly from VS Code's built-in new file menu
- New keyboard shortcuts: `Cmd+K, Cmd+I` (Indicator) and `Cmd+K, Cmd+S` (Strategy) on macOS; `Ctrl+K, Ctrl+I` / `Ctrl+K, Ctrl+S` on Windows and Linux

### Fixed
- False errors on typed variable declarations (`int x = ...`, `float y = ...`) when the script uses `import`
- False errors on identifiers inside function bodies that used mixed tab/space indentation
- "Open external website" dialog no longer appears when clicking CodeLens entries
- Removed Library template (not supported in this release)

## [0.9.3] 2026-06-09

### Fixed
- Syntax error detection was not working — standalone invalid identifiers and other structural errors were not reported. Now all syntax checks work correctly.

## [0.9.2] 2026-06-09

### Fixed
- False "trailing comma" error on calls where the last argument is a string literal (e.g. `hline(0, "Zero line")` was incorrectly flagged)
- Extension stability: the extension host no longer crashes when opening complex or mixed-indentation Pine Script files

## [0.9.1] 2026-06-09

### Fixed
- False "used before declaration" errors on `obj.field` property accesses — the extension no longer flags a field name (e.g. `currentTrail.bias`) as a forward reference to a same-named global variable
- False "bare number literal" errors were possible on single-quoted strings containing a word followed by a digit (e.g. `'Level 0'`) — now correctly ignored

## [0.9.0] 2026-06-09

### Added
- IntelliSense now includes your own functions, variables, types and parameters — autocomplete works across the entire file, not just built-ins
- Function parameters appear in completions inside the function body
- Hover tooltips now show documentation for user-defined symbols

### Improved
- Diagnostics catch more real-world Pine Script mistakes: `varip` inside functions, `strategy.*` calls in indicators, `input.*` inside `if`/`for` blocks, Unicode characters that TradingView rejects, variables used before declaration, and duplicate `var` declarations

## [0.8.9] 2026-06-08

### Added
- **Bare number literal detection** — flags a number literal that appears directly after an identifier without an operator (e.g. `ft4 4562`), which causes "Syntax error at input" in TradingView; only checks non-indented top-level lines to avoid false positives in multi-line expressions
- **Invalid statement detection** — flags a standalone identifier at the global scope (e.g. `gdgdfs` on its own line) which causes `"gdgdfs" is not a valid statement` in TradingView; does not flag inside function bodies where a bare identifier is a valid return value

### Improved
- Test coverage expanded to 139 tests

## [0.8.8] 2026-06-07

### Added
- **Non-ASCII character detection** — flags Unicode homoglyphs (`×`, `–`, `—`, `≥`, etc.) in code that TradingView rejects at compile time; suggests the correct ASCII equivalent; skips characters inside comments and string literals
- **`varip` in function body** — flags `varip` used inside a user-defined function (only valid at global scope)
- **`strategy.*` in non-strategy script** — flags `strategy.entry()`, `strategy.close()`, etc. inside `indicator()` or `library()` scripts
- **`input.*` inside `if`/`for` block** — flags `input.int()`, `input.float()`, etc. called inside conditional or loop blocks (must be at global scope)

### Improved
- Test coverage expanded to 132 tests — all diagnostic codes now have full positive and negative test cases

## [0.8.7] 2026-06-07

### Added
- **User-defined symbol support** — IntelliSense now understands your own functions, variables and types
  - Completion, hover and signature help work for user-defined functions (with full parameter list)
  - Hover shows fields for User-Defined Types (`type MySignal ...`)
  - UDT field and method completion after `myVar.` when the type is known
  - Completion shows user variables with inferred or declared type
- **3 new diagnostics**
  - `varip` inside a function body → error (only valid at global scope)
  - `strategy.*()` calls inside `indicator()` or `library()` scripts → error
  - `input.*()` calls inside `if` / `for` blocks → error (must be at top level)

## [0.8.6] 2026-06-06

### Improved
- Diagnostics are smarter about `or`/`and` line continuation — no false warnings when the expression is inside parentheses
- Diagnostics no longer flag function parameters as undeclared variables
- Diagnostics correctly detect duplicate `var` declarations in the same scope

## [0.8.5] 2026-06-06

### Added
- Diagnostics now warn when a variable is used before it is declared
- Diagnostics now detect `or`/`and` at the start of a continuation line — a common Pine Script syntax mistake

### Improved
- Internal code quality improvements across all providers

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
- Diagnostics no longer flag commented-out lines as errors — only real code is analyzed

## [0.8.1] 2026-06-06

### Improved
- Marketplace page updated with clearer description, better structure and improved readability
- Fixed failing tests caused by publisher ID mismatch after marketplace migration

## [0.8.0] 2026-06-06

### Improved
- Syntax highlighting now correctly recognizes generic type angle brackets such as `array<float>` and `matrix<int>`
- Bracket and punctuation characters are styled consistently in both Dark and Light themes
- Bracket pair colorization is disabled by default to avoid conflicts with Pine Script syntax colors

## [0.7.0] 2026-06-05

### Changed
- Performance improvements with faster symbol lookups across all providers
- Internal refactoring for stability and correctness

## [0.6.0] 2026-06-05

### Added
- **Find All References** (Shift+F12) finds all usages of any user-defined symbol
- **Clickable Links** TradingView URLs in comments are now hyperlinks
- **Color Picker** inline color picker for `color.rgb()` and all `color.*` constants
- **Format Document** normalizes indentation, trims trailing whitespace, collapses excess blank lines
- **Getting Started Walkthrough** 4-step onboarding in the VS Code Help tab
- 3 new settings: `pinescript.references.enable`, `pinescript.color.enable`, `pinescript.formatting.enable`

## [0.5.0] 2026-06-05

### Added
- **Rename Symbol** (F2) renames any user-defined symbol across the file
- **Smart Folding** folds function bodies, `type` blocks, multiline `indicator()` calls and `// #region` markers
- **Code Lens** shows usage count above every user-defined function
- **Pine Script Explorer** Activity Bar sidebar to browse all built-in namespaces and insert symbols

## [0.4.0] 2026-06-05

### Added
- **Real-time Diagnostics** squiggly lines for missing `//@version=6`, missing `overlay=`, `request.security()` in loops, `plot()` in `if` blocks
- **Go to Definition** (F12) jumps to user-defined symbols and opens TradingView docs for built-ins
- **Document Highlight** highlights all occurrences of the symbol under cursor in real time
- **Status Bar** shows `Pine Script v6` or a warning for every active `.pine` file
- **Open on TradingView** button in the editor title bar
- 4 new settings for diagnostics, hover links and completions

## [0.3.0] 2026-06-04

### Changed
- Smaller VSIX package size
- Faster extension activation

## [0.2.0] 2026-06-04

### Added
- **Document Outline** shows functions, variables, UDTs and inputs in breadcrumbs and the Outline panel
- **Code Actions** quick fixes to add `//@version=6`, add `overlay=`, or wrap with `barstate.isconfirmed`
- **Semantic Highlighting** colors user-defined functions, variables, types and parameters distinctly
- **@pinescript Chat** AI assistant in Copilot Chat with `/explain`, `/indicator`, `/strategy` commands

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
