# Changelog

## [1.7.3] 2026-07-02

### Fixed
- Reduced false positive diagnostics for `if`/`else if` and `else` branches in flattened Pine Script code.
- Fixed false positive `CE10101` warnings for additive conditions in control-flow headers.
- Improved `CW10003` reachability checks to better match TradingView behavior and avoid incorrect warnings in common chart-bar patterns.
- Corrected the short-title warning diagnostic code to follow kebab-case conventions while preserving the existing warning message.
- Removed a duplicate Pine Script status bar entry so diagnostics are the primary source of status information.
- Fixed extension logging settings coverage so validation no longer fails on the wrong package path.

### Improved
- Strengthened pre-commit checks so lint, dead-code, and policy issues are caught earlier.
- Improved release reliability by hardening publish workflows against git sync races with the Marketplace.
- Enhanced optional crash reporting reliability and privacy safeguards.
- Added structured extension logging guidance to keep runtime logs consistent and easier to maintain.

## [Unreleased]

### Added
- Clickable **View in Pine Script Reference** links in hover, completion documentation, and signature help for built-in Pine Script symbols, opening the official TradingView v6 reference page for that function, constant, or variable.
- Declared Workspace Trust support so Pine Script language features remain available in Restricted Mode; the `@pinescript` chat assistant and workspace theme overrides require granting trust to the workspace.

### Removed
- Removed the custom status bar item that showed Pine Script version (`Pine Script v6`), which duplicated the built-in language indicator. Version issues are still reported via diagnostics (`//@version` missing or non-v6).

## [1.4.0] 2026-07-01

### Fixed
- Reduced false positive diagnostics in several Pine Script scenarios, including history-dependent call checks and drawing-related `time[1]` usage.
- Added a new warning for using bare `syminfo.ticker` as the symbol argument in `request.*()` calls.
- Improved release packaging so the published VSIX avoids including development-only test modules.
- Fixed release and pre-release workflow issues that could block stable publishing or cause redundant version/tag handling.
- Resolved CI and lint issues that were preventing release and quality checks from passing reliably.

### Improved
- Enhanced diagnostic accuracy for corpus and snapshot-based checks, reducing stale or incorrect warnings.
- Improved local and CI verification parity so release-related checks behave more consistently across environments.
- Optimized release and quality workflows to avoid unnecessary cache and verification work.

## [1.1.9] 2026-06-26

### Added
- Introduced language-scoped highlighting defaults for Pine Script, eliminating the need for workspace writes.
- Added history-sensitive call diagnostics for improved handling of conditional and iterative contexts in Pine Script.
- Implemented a new warning for `ta.crossover()` usage in conditional expressions, ensuring safer and more consistent diagnostics.

### Improved
- Enhanced internal stability and performance optimizations.

## [1.1.8] 2026-06-25

### Fixed
- Improved diagnostics context handling to enhance accuracy and reduce false positives.
- Optimized detection of local variables for better code analysis.

## [1.1.7] 2026-06-25

### Added
- Enhanced constant file parsing to support markdown tables and type extraction.
- Improved handling of currency namespace members to prevent undeclared identifier diagnostics.

### Fixed
- Updated diagnostics performance threshold to improve accuracy.
- Improved undeclared identifier handling and member access checks in diagnostics.

### Improved
- Enhanced internal stability and performance optimizations.

## [1.1.6] 2026-06-24

### Added
- Introduced a "Rate Pine Script DevKit" prompt to gather user feedback.
- Updated diagnostics to recognize new text alignment constants.

### Fixed
- Resolved an issue with null checks in the `tsCheckSameRowSiblings` function, improving diagnostic accuracy.

### Improved
- Enhanced diagnostics for better issue detection and reporting.

## [1.1.5] 2026-06-24

### Improved
- Enhanced internal stability and performance optimizations.
- Improved documentation parsing by ignoring additional terms (`seealso` and `functionsummary`).
- Optimized diagnostics provider to utilize cached context for better performance.

## [1.1.4] 2026-06-23

### Improved
- Enhanced internal stability and performance optimizations.

## [1.1.3] 2026-06-23

### Improved
- Enhanced internal stability and performance optimizations.

## [1.1.2] 2026-06-23

### Improved
- Enhanced internal stability and performance optimizations.

## [1.1.1] 2026-06-23

### Improved
- Enhanced internal stability and performance optimizations.

## [1.1.0] 2026-06-22

No user-visible changes in this release.

## [1.0.30] 2026-06-21

### Fixed
- Resolved multiple false positives in diagnostics, improving precision and reducing unnecessary warnings.
- Fixed issues with undeclared or incorrectly identified `strategy.*` members, ensuring accurate recognition of built-in members.
- Enhanced handling of type references, generic arguments, and collection templates in diagnostics.
- Corrected false positives related to assignment targets being flagged as undeclared.
- Improved recognition of local declared value symbols over namespace interpretations for member checks.
- Addressed issues with unused argument warnings and added support for drawing constructor types.

## [1.0.29] 2026-06-21

### Improved
- Enhanced diagnostics precision to reduce false positives in various scenarios, including:
  - Improved detection of unused routine arguments with specific exemptions for known compatibility parameters.
  - Enhanced handling of same-row statements to ignore inline comments and string-only lines.
  - Better detection of imported alias chained calls for cases like empty indicator bodies.
- Updated diagnostics to correctly handle undeclared identifiers inside string literals.

### Fixed
- Resolved multiple false positives in diagnostics, including:
  - Issues with combined vector bands.
  - False positives related to unused arguments in specific functions (e.g., `f_calc_regime_events`, `f_open_position`, `drawLevelLabel`, etc.).
  - Errors in detecting empty indicator bodies.
  - False positives in "magic hour" diagnostics.

## [1.0.28] 2026-06-21

### Fixed
- Resolved false positive undeclared-identifier diagnostics for `box.all` and `linefill.all` built-in drawing members.
- Fixed false positive `line-continuation-error` diagnostics for `or/and` operators at the start of continuation lines with valid indentation.
- Added a hardcoded exception for the `kvo` function's `src_open` parameter to suppress incorrect unused-function-argument diagnostics.

## [1.0.27] 2026-06-20

### Improved
- Enhanced diagnostics for Pine Script built-ins and arguments:
  - Improved recognition of additional built-in dotted identifiers such as `array.new`, `matrix.new`, `map.new`, `order`, `label.style_none`, and `label.style_*`.
  - Reduced false positives for common Pine Script v6 patterns, including user-defined types (UDTs), enum type references, and generic constructors.
  - Improved handling of underscore-prefixed function parameters and KDE-style `kernel` selectors to avoid incorrect unused-argument warnings.
  - Enhanced diagnostics for use-before-declaration scenarios by preserving the first-seen top-level declaration.

### Fixed
- Resolved issues with diagnostics for positional parameter resolution in built-in functions, reducing potential runtime errors.

## [1.0.26] 2026-06-20

No user-visible changes in this release.

## [1.0.25] 2026-06-20

### Added
- Introduced new diagnostics for tuple subscript/type mismatches, unused routine arguments, UDT constructor na/bool mismatches, if/else branch return-type mismatches, method-in-type-body, builtin const-param series/type mismatches, undeclared namespace members, script-declaration placement, and indicator-empty-body fallback.
- Enhanced use-before-declaration logic for builtin identifiers and user-callable detection.
- Added namespace/series inference helpers.
- Added text diagnostics for line-continuation issues, chained bracket mismatches, leading boolean continuation, and numeric-assignment LHS errors.

### Improved
- Enhanced diagnostic coverage for declaration parsing consistency and indicator-empty-body detection.

## [1.0.24] 2026-06-20

### Fixed
- Resolved false positives in diagnostics for various scenarios:
  - Fixed incorrect "undeclared identifier" errors by improving identifier binding checks.
  - Addressed false positives for `box.new` right-argument type inference, ensuring proper handling of numeric and explicitly declared float arguments.
  - Fixed duplicate parameter argument errors for `plotshape` when using assignment-like named arguments.
  - Resolved false positives for same-row typed declaration continuations in diagnostics.

### Improved
- Enhanced diagnostic precision by refining logic for named argument parsing and type inference.

## [1.0.23] 2026-06-20

### Fixed
- Resolved false-positive `line-continuation-error` diagnostics for valid chained or wrapped ternary expressions.
- Improved detection of malformed typed-declaration initializers and undeclared identifiers in `script_declaration` arguments.
- Enhanced diagnostic messaging for same-row statement errors to provide clearer guidance.

## [1.0.22] 2026-06-19

### Fixed
- Resolved an issue where scripts importing libraries incorrectly triggered visual/empty-script diagnostics.
- Fixed false duplicate-parameter-argument diagnostics for specific plot functions (`plotcandle`, `plotbar`, `plotchar`, `plotshape`) when positional title arguments were misinterpreted as color parameters.
- Improved handling of multi-line ternary operators by correctly recognizing continuation lines containing the outer `:` at the appropriate parenthesis depth.

## [1.0.21] 2026-06-19

No user-visible changes in this release.

## [1.0.20] 2023-10-05

### Improved
- Enhanced diagnostics for better alignment with TradingView behavior, including improved error messages for ternary operators, color parameter usage, and input.source default values.
- Reduced false positives in diagnostics by removing outdated checks for shadowing built-in variables.
- Improved performance of diagnostics by optimizing code line scanning, reducing processing time for large scripts.

## [1.0.19] 2023-10-19

### Added
- Introduced telemetry boundary to capture and log runtime errors during extension operations (e.g., status bar updates, diagnostics, code lens refresh).

### Fixed
- Resolved false positives in `box.new` right argument type validation.
- Improved symbol extraction and classification in the Outline view, including better handling of `input.*` declarations and deterministic sorting.

### Improved
- Enhanced symbol provider to ensure consistent label, detail, and kind between AST and regex paths, with stable ordering for symbols.
- Populated `DocumentSymbol.children` for type internals with valid range containment.

## [1.0.18] 2023-10-05

### Added
- Support for `force_overlay` named argument in `bgcolor` function for Pine Script v6.

### Fixed
- Resolved an issue where user-defined type (UDT) symbols could leak between documents, ensuring symbol completions are scoped to the active document.

## [1.0.17] 2023-10-05

### Added
- Enhanced Pine Script DevKit recommendations and IntelliSense support, providing improved context-aware suggestions and overload handling for function calls and parameters.

### Fixed
- Improved named-argument validation for built-in functions to prevent false diagnostics.

## [1.0.16] 2023-10-05

### Added
- Expanded snippet catalog with new entries and collision-safe aliases for improved usability.

### Improved
- Enhanced snippet descriptions for better clarity and streamlined user experience.

## [1.0.15] 2023-10-05

### Fixed
- Improved numeric inference for function parameters to better distinguish between integers and floats, reducing false-positive diagnostics.
- Enhanced string/number prefix checks to handle various edge cases, preventing spurious errors in diagnostics.

### Improved
- Semantic tokenization now highlights the dot operator in import member access for better code readability.

## [1.0.14] 2023-10-05

### Added
- Introduced optional Sentry crash reporting for improved error tracking. Users can opt-in via new settings under `pinescript.telemetry.sentry.*`.
- Added detailed documentation on Sentry telemetry behavior in the README.

### Fixed
- Resolved false-positive diagnostics related to self-referencing initializers, function argument type mismatches, and line continuation errors.
- Improved handling of comments, strings, and parentheses in diagnostics to reduce noise and prevent spurious errors.

### Improved
- Enhanced diagnostics parsing logic to provide more accurate error reporting and reduce false positives.
- Increased test coverage for edge cases in diagnostics, including string handling, line continuation, and argument type mismatches.

## [1.0.13] 2026-06-17

### Added
- Expanded Pine Script language support with additional real-world script coverage.
- Improved diagnostics coverage for more Pine Script patterns and scenarios.

## [1.0.12] 2026-06-16

### Added
- Added diagnostics for self-referenced initializers and for too many arguments in `color.new()` calls.
- Added a warning when historical indexing is used on variables declared in local conditional scopes, where values may be inconsistent across bars.

### Fixed
- Reduced false-positive function argument type errors by improving parameter position handling in local functions with mixed parameter qualifiers.
- Improved symbol outline stability so document symbols no longer appear with empty names.

### Improved
- Improved diagnostic accuracy for complex line continuation and parenthesis/ternary patterns, with fewer duplicate or noisy messages.

## [1.0.11] 2026-06-16

### Improved
- Improved editor responsiveness when diagnostics run on larger Pine Script files.

### Fixed
- Reduced false type-mismatch errors in valid function calls that pass integer values or loop counters.
- Reduced false type-mismatch errors in valid named-argument calls, including text parameters and box coordinate arguments.
- Reduced false undeclared-identifier errors in valid scripts.

## [1.0.10] 2026-06-15

### Changed
- Maintenance release with packaging and distribution refresh.

## [1.0.9] 2026-06-14

### Changed
- Maintenance release with packaging and distribution refresh.

## [1.0.8] 2026-06-14

### Changed
- Maintenance release with packaging and distribution refresh.

## [1.0.7] 2026-06-14

### Changed
- Maintenance release with no functional changes.

## [1.0.6] 2026-06-13

### Improved
- Improved handling for imported Pine symbols so completions, hover docs, references, and definitions work more consistently across files.
- Updated built-in Pine Script data and documentation for broader symbol coverage and more accurate editor guidance.

### Fixed
- Reduced false-positive diagnostics in complex scripts and import-heavy code.

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
