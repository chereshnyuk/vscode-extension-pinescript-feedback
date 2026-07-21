# Changelog

## [Unreleased]

### Added

- Type mismatch detection for four cases TradingView rejects but the editor previously accepted: conditional branches that cannot share a type such as `close > 0 ? 1 : "a"`, assignments and typed declarations whose value does not fit the variable such as `int x = 1.5`, operators applied to incompatible values such as `"text" + close`, and built-in call arguments whose type or qualifier does not match the parameter such as `plot("hello")` or a bar-varying length passed to `ta.ema`.
- These checks stay quiet whenever a type cannot be determined confidently, so unfamiliar or partially written code is not flagged on a guess.

### Changed

- Argument type problems now report under a single code, `argument-type-mismatch`. It replaces four narrower codes (`box-right-arg-type-mismatch`, `builtin-param-qualifier-mismatch`, `builtin-const-param-series-mismatch`, `function-arg-type-mismatch`), which are no longer reported. If you filter or suppress problems by code, update those entries. The checks themselves were not removed — they were folded into the general argument check, which now also covers calls the old ones missed: overloaded built-ins such as `box.new` and `label.new`, script declarations, and the types of your own function parameters.

### Fixed

- Switch blocks whose body begins with a comment are now read correctly. Previously the entire block could be misread, hiding its contents from analysis and producing misleading results.
- Arguments to overloaded built-ins are matched against the specific overload being called, so a call such as `timestamp("America/New_York", 2020, 1, 1)` is no longer misread against a different overload's parameters.
- More accurate type reasoning in several places: dividing two whole numbers now yields a whole number, results of functions such as `math.max` and `nz` keep the stability of their arguments, and a call to your own function is no longer mistaken for a built-in that happens to share its short name.
- Corrected the types of built-in variables so type-aware diagnostics judge them accurately. Symbol information such as `syminfo.ticker` and `syminfo.prefix` was previously recorded as a number rather than text, which could make correct code look wrong.
- Filled in the argument types of built-in functions, so argument checks now cover most parameters instead of a minority of them.
- Scripts that reference built-in functions which do not exist in Pine v6 such as `color.hsv` or `label.set_url` are now flagged as unknown instead of being accepted silently.

### Improved

- Built-in symbol types, descriptions, and signatures now come from the official Pine Script v6 reference, so hover and completion information matches TradingView more closely.

## [2.7.0] 2026-07-19

### Changed

- Removed the "Pine Script:" prefix from command titles so commands stay grouped under their category in the command palette.
- Aligned diagnostic message wording with TradingView for closer consistency with the official checker.
- Standardized diagnostic message formatting with a uniform code suffix and added consistent punctuation to setting descriptions.

### Improved

- Updated translations across all supported languages for command titles, setting descriptions, and diagnostic messages.
- Faster diagnostics on large multi-routine scripts with significantly reduced processing time per run.
- Optimized diagnostics analysis to lower memory use and improve responsiveness while editing.

## [2.6.4] 2026-07-19

### Added

- Expanded the bundled remote library cache so more imported Tier 2 libraries resolve offline without a network connection.

### Fixed

- Corrected resolution of remote libraries that share case-variant names so imports now match the correct published library and version.
- Resolved false not-found results for libraries whose authors were renamed so those imports resolve again.

### Improved

- Refreshed cached remote libraries so previously unresolved imports no longer report resolution hints.
- Optimized diagnostics performance for files that use imported libraries for faster and more responsive analysis.

## [2.6.3] 2026-07-19

### Added

- Diagnostics now analyze the effects of resolved external library members so warnings match TradingView on scripts that rely on shared libraries.

### Fixed

- Corrected metadata for time_tradingday and timenow so their type is reported as series int.
- Corrected metadata for the timeframe.is family of variables so their type is reported as simple bool.

### Improved

- Aligned error cascade behavior with TradingView so uses that depend on a failed declaration are reported consistently.
- Improved diagnostic line and column reporting for statements wrapped across multiple lines so positions match TradingView.
- Refined guard detection for not na checks and compound or conditions so history related warnings match TradingView more closely.
- Reduced stale resolution hints and improved overall diagnostic accuracy against TradingView.
- Optimized diagnostic type resolution for faster and more responsive analysis.

## [2.6.1] 2026-07-18

### Improved

- Improved accuracy of syntax error detection to better match TradingView behavior, including typed tuple destructuring errors and extra closing parenthesis errors.

### Fixed

- Fixed a false positive where comma-joined statements on the same row could be incorrectly flagged.

## [2.6.0] 2026-07-18

### Added

- Pine agent tools are now available to any MCP-capable host in the same VS Code window through a built-in server that you can turn on with the pinescript.mcp.enable setting.
- New command Pine Script: Generate Agents Guidance writes a Pine workflow guidance section into your AGENTS.md file.
- Added a builtin search tool that ranks fuzzy matches over local Pine metadata.
- Added a workspace diagnostics tool that scans across your workspace for issues.
- Localized 15 new or updated strings across all 14 supported languages.

### Changed

- Marketplace listing now includes AI and Chat categories along with new keywords, and the README highlights both Copilot and MCP support for all seven agent tools.

### Fixed

- Corrected wording in agent guidance content so it stays accurate in shipped builds.

### Improved

- Crash-free user and affected-user reporting is now more accurate through anonymous session identification, while email, username, and IP data remain stripped.

## [2.5.4] 2026-07-17

### Added

- Warnings now flag history-dependent calls in switch dispatch over typed selectors such as string or enum parameters, matching TradingView behavior.
- Warnings now cover history-dependent calls under bare bool parameters in ternary and if-guard usage, matching TradingView behavior.

### Fixed

- Corrected parsing of switch arms whose body ends with a comma-separated value after an assignment so later arms are no longer dropped.
- Color swatches and usage counts no longer appear for matches inside strings and comments.

### Improved

- Improved accuracy of type and numeric inference for more reliable diagnostics.

## [2.5.3] 2026-07-16

### Fixed

- Fixed incorrect configuration-vs-series warnings when conditions compare against global constants.
- Fixed qualifier diagnostics for `var` and `varip` values so reassigned persistent values are handled correctly.
- Fixed false argument-type warnings for supported collection arguments.

### Improved

- Improved diagnostic accuracy for Pine v6 built-ins and qualifier handling.
- Improved telemetry reliability for desktop extension sessions and disabled unsupported telemetry behavior in web environments.

## [2.5.2] 2026-07-16

### Improved

- Enhanced internal stability and performance optimizations.

## [2.5.1] 2026-07-16

### Added

- Added localized quick-fix guidance for undeclared identifier diagnostics.

### Fixed

- Fixed undeclared identifier diagnostics to better match TradingView behavior across global scopes, blocks, functions, and methods.
- Fixed false CW10003/CW10004 warnings for configuration comparisons and related guard conditions.

### Improved

- Optimized diagnostics performance and responsiveness for larger scripts.

## [2.5.0] 2026-07-15

### Fixed

- Restored warning parity for Combined Vector Bands and related conditional and loop patterns.
- Fixed missed history-dependent warnings when `var` or `varip` boolean guards are reassigned later.
- Fixed stale line tracking after multi-edit changes so diagnostics and semantic highlighting update the correct lines.
- Fixed a session issue where language intelligence could remain unavailable after a startup failure instead of recovering on retry.
- Fixed incorrect analysis results that could occur with chained field access expressions.

### Improved

- Improved responsiveness of signature help and completions for incomplete function calls in large files.
- Improved editor responsiveness by cancelling superseded background analysis while documents are changing.
- Improved memory cleanup during repeated editing and symbol analysis.

## [2.4.2] 2026-07-14

### Fixed

- Reduced incorrect CW10003 warnings for selector-less boolean-guard switch patterns, aligning diagnostics more closely with TradingView behavior.
- Reduced incorrect CW10003 warnings for drawing-handle lifecycle patterns.
- Reduced incorrect CW10013 shadowing warnings for variables declared in mutually exclusive `if` branches.

## [2.4.0] 2026-07-14

### Added

- Added a diagnostic for unterminated string literals in Pine v6 files.

### Fixed

- Fixed string literal handling so `//` inside quoted text is no longer treated as a comment.
- Fixed missing consistency warnings for some fixed-lag built-in routine reads.
- Fixed false consistency warnings for fixed-lag routine reads that match Pine runtime behavior.
- Fixed false local-history warnings in nested conditions.
- Fixed a false consistency warning for branch-local reassignments of untyped parameters.
- Fixed false CW10003 warnings on inline drawing lifecycle helpers (`label.delete(label.new(...)[1])`) under `barstate.islast` (dna bands parity).
- Fixed false CW10003 warnings on built-in `ta.*` calls in routine assignment short-circuit chains where TradingView emits CW10002 only.

## [2.3.4] 2026-07-12

### Fixed

- Fixed an activation error that affected chat participant disambiguation on desktop and web.
- Fixed incremental diagnostics so structural edits and coalesced changes update affected warnings more reliably.

### Improved

- Improved extension responsiveness when restoring workspaces with many open Pine documents.
- Improved diagnostics performance during editing by reducing repeated work on incremental updates.
- Improved cancellation behavior for long-running editor requests such as references, rename, completions, inlay hints, and code lenses.
- Improved workspace symbol updates so in-editor changes are reflected before saving.

## [2.3.3] 2026-07-12

### Added

- Added visible Marketplace, security scan, license, and Pine v6 support badges to the README.
- Added public VirusTotal report links for release artifacts.

### Fixed

- Reduced false-positive diagnostics for valid Pine history and conditional expression patterns.

### Improved

- Refined the Marketplace description and localized extension metadata to better explain the extension's value.
- Improved README organization for clearer onboarding and setup flow.
- Improved Marketplace presentation with clearer chat participant wording and settings ordering.

## [2.3.0] 2026-07-11

### Fixed

- Fixed missing companion diagnostics so related Pine Script warnings are reported together.
- Reduced duplicate diagnostics in the Problems panel.
- Fixed false positive warnings for valid Ribbon/bar-variant conditions.

### Improved

- Diagnostics now appear sooner when opening Pine Script files, especially on larger files.
- Improved built-in Pine Script reference descriptions and documentation links.

## [2.2.12] 2026-07-11

### Improved

- Reduced false positives in history-related diagnostics to better match TradingView behavior.
- Improved diagnostic consistency for conditional and ternary history checks, including better handling of nested and chart-scope cases.
- Enhanced stability and reliability of diagnostic reporting for imported calls, security expressions, and variable state lifecycle guards.

## [2.2.11] 2026-07-10

### Fixed

- Refactored CW10004 lazy ternary diagnostics to a unified `classifyTernaryBranchRelation` model, replacing the per-corpus exemption zoo.
- Fixed false positive CW10004 on config-gated passthrough smoothing ternary patterns in supertrend-style scripts.
- Reduced false positive CW10004 diagnostics for configuration-selector ternary patterns.

## [2.2.10] 2026-07-10

### Fixed

- Reduced false positive CW10004 diagnostics for nested input-gated moving-average selector patterns.
- Updated GitHub links and marketplace-related URLs to the renamed account.

## [2.2.9] 2026-07-08

### Improved

- Reduced false positives in lazy-evaluation diagnostics for ternary branches inside pure wrapper calls, including cases involving `nz` and `ta.*` expressions.
- Improved reachability diagnostics so short-circuit conditions are handled more consistently in `and`/`or`-only scripts.
- Refined history-based diagnostics to better match TradingView behavior for structural reachability and ternary evaluation patterns.
- Updated diagnostic baselines to reflect the latest false-positive reductions and reachability refinements.

## [2.2.7] 2026-07-08

### Fixed

- Reduced false positive CW10003 diagnostics for drawing routines, including cases where drawing handles are rebound without depending on prior history.
- Improved CW10003 handling for nested routine call tracing so switch-arm reachability is analyzed more accurately.

## [2.2.6] 2026-07-07

### Fixed

- Reduced false CW10003 diagnostics for configuration-based switch dispatch, including nested helper chains and overloaded routines.
- Improved parity with TradingView by keeping valid MA-selector and session-reset switch patterns from being flagged.
- Allowed comments between switch arms without triggering CW10003 in supported cases.

### Improved

- Enhanced diagnostics performance and responsiveness.
- Improved release stability by rebalancing diagnostics performance thresholds to reduce CI flakiness.

## [2.2.3] 2026-07-06

### Fixed

- Reduced false positive diagnostics for certain `ta.*` composition patterns that use historical series access, so feature-toggle logic is less likely to be flagged incorrectly.
- Improved switch-based `ta.*` history checks to better match TradingView behavior, reducing incorrect diagnostics in those cases.
- Fixed release publishing so the extension no longer runs the same prepublish build step twice during marketplace release workflows.

### Improved

- Enhanced internal stability and performance optimizations.

## [2.2.0] 2026-07-05

### Improved

- Release publishing now cleans up failed release tags automatically, helping prevent blocked re-dispatches after publish failures.
- Release verification now catches production bundle allowlist drift earlier, reducing the chance of shipping unexpected artifacts.
- Test runs now clean up temporary artifacts more reliably, improving local and CI test stability.

## [2.1.0] 2026-07-05

### Fixed

- Reduced false positives in history-sensitive diagnostics for nested wrapper calls.
- Restored a missing diagnostic for compound conditions that combine input and series checks.
- Fixed false positives in loop-end shadowing detection for subtractive `for` ranges.
- Corrected detection of typed tuple destructuring so the related diagnostic appears again.
- Improved theme readability for generic type angle brackets in light themes.
- Removed a noisy editor title-bar formatting entry while keeping formatting available from commands.
- Trimmed redundant activation events so the extension relies on VS Code’s implicit activation behavior.

### Improved

- Improved diagnostic performance on simple lines by skipping unnecessary scanning work.
- Strengthened the text diagnostics performance guard to better catch scaling regressions.
- Optimized internal diagnostics context reuse for better responsiveness.
- Reduced extension package size by excluding unnecessary bundled content from the VSIX.
- Tightened coverage and release checks to keep quality gates stable.

## [2.0.5] 2026-07-04

### Fixed

- Restored a missing diagnostic for conditional `request.security` call sites so history-dependent warnings match TradingView behavior more closely.
- Improved the visibility of Pine Script parentheses in the light theme so they remain readable.
- Fixed the “What’s New” notification so release notes and additional actions no longer overflow or clip.
- Ensured localization files are included correctly in release packages.

## [2.0.7] 2026-07-05

### Improved

- Added `workspaceContains:**/*.pine` activation so Pine Script DevKit warms language services when a workspace folder contains Pine Script files, even before a `.pine` editor is opened.
- Deferred what's-new and automatic walkthrough onboarding until Pine editor context appears so workspace-only activation does not surface intrusive UI.

## [2.0.6] 2026-07-05

### Improved

- Hardened Marketplace **FEATURES** metadata: full command activation coverage including **View Release Notes**, localized Language Model Tool `modelDescription` strings, `Shift+Alt+F` format keybinding for Pine editors, and theme defaults synced from canonical theme JSON via `npm run sync:manifest-theme-defaults`.
- Added README **Marketplace FEATURES Reference** mapping each FEATURES sidebar category to user-facing capabilities.

### Fixed

- Fixed lazy activation gap for `pinescript.viewReleaseNotes` when what's-new or deep-link flows run before a `.pine` file is opened.

## [2.0.2] 2026-07-03

### Improved

- Improved release packaging checks so published builds are less likely to fail on bundled AI-related assets.
- Enhanced stability and reliability for the extension’s shipped language features.

## [2.0.1] 2026-07-03

### Fixed

- Fixed release verification so the web extension bundle and VSIX contents are checked against the correct shipped outputs.
- Improved release recovery guidance when a Marketplace publish is behind the git history.

## [2.0.0] 2026-07-03

### Added

- Added document links, on-type formatting, type definitions, inlay hints, and opt-in inline completions for Pine Script.
- Added workspace symbols, selection range support, and format selection support for Pine Script.
- Added semantic token delta updates for smoother syntax highlighting.
- Added virtual workspace support for local Pine imports.
- Added AI-assisted Pine Script tools, chat prompts, and guided onboarding content.

### Fixed

- Fixed a false positive diagnostic for `ta.barssince` inside user-defined functions.
- Fixed reference links in hover, completion, and signature help so they respect the setting to hide TradingView URLs.
- Fixed packaging metadata so the extension presents accurate marketplace information.
- Fixed the extension so local import handling works correctly in virtual workspaces.

### Improved

- Improved editor responsiveness and language feature coverage across common Pine Script workflows.
- Improved extension reliability and packaging for Marketplace distribution.
- Improved support for web usage and reduced unnecessary VSIX contents.

## [1.8.0] 2026-07-03

### Added

- Language Model Tools for Copilot Agent mode: `#pinescript_lookup_builtin`, `#pinescript_get_diagnostics`, and `#pinescript_scaffold` backed by local Pine metadata and diagnostics.
- Explorer context menu entries for **Pine Script: New Indicator** and **New Strategy**, plus editor title **Format Document** for `.pine` files.
- CHANGELOG-aware what's-new notification with **View Release Notes** action after updates.

### Improved

- `@pinescript` chat participant now uses editor selection for `/explain`, suggests follow-up prompts, and honors attached Agent tool references.
- Walkthrough refreshed with diagnostics, formatting, and Agent tools steps aligned to the current product surface.
- Explicit lazy `activationEvents` and `Machine Learning` marketplace category for AI contributions.

## [1.7.6] 2026-07-03

### Fixed

- Reduced false positive diagnostics for `request.security`-related code, making history and reachability checks more accurate.
- Fixed VSIX verification so releases include the newly added localization file without failing validation.

### Added

- Added limited support for virtual workspaces in the extension manifest.

## [1.7.5] 2026-07-03

### Added

- TradingView reference links now appear in IntelliSense, hover details, and signature help for built-in functions.
- Workspace Trust support keeps language features available in Restricted Mode, while chat and workspace theme overrides remain gated until trust is granted.

### Fixed

- Reduced false positives for CW10003 on `ta.highest` and `ta.lowest` helpers called only inside `request.security` expressions, including Donchian and HTF cache patterns.
- Reduced false positives for CW10003 on transitive drawing-only routines.
- Improved CW10004 behavior for user-defined security wrappers in lazy ternaries so warnings better match the intended parity rules.

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

## [1.4.0] 2026-07-01

### Fixed

- Reduced false positive diagnostics in several Pine Script scenarios, including history-dependent call checks and drawing-related `time[1]` usage.
- Added a new warning for using bare `syminfo.ticker` as the symbol argument in `request.*` calls.
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
- Implemented a new warning for `ta.crossover` usage in conditional expressions, ensuring safer and more consistent diagnostics.

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
- Improved documentation parsing by ignoring additional terms `seealso` and `functionsummary`.
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
  - False positives related to unused arguments in specific functions such as `f_calc_regime_events`, `f_open_position`, and `drawLevelLabel`.
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
  - Reduced false positives for common Pine Script v6 patterns, including user-defined types, enum type references, and generic constructors.
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
- Fixed false duplicate-parameter-argument diagnostics for specific plot functions when positional title arguments were misinterpreted as color parameters.
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

- Introduced telemetry boundary to capture and log runtime errors during extension operations such as status bar updates, diagnostics, and code lens refresh.

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

- Resolved an issue where user-defined type symbols could leak between documents, ensuring symbol completions are scoped to the active document.

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

- Added diagnostics for self-referenced initializers and for too many arguments in `color.new` calls.
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
- New keyboard shortcuts on macOS: `Cmd+K, Cmd+I` for Indicator and `Cmd+K, Cmd+S` for Strategy.
- New keyboard shortcuts on Windows and Linux: `Ctrl+K, Ctrl+I` for Indicator and `Ctrl+K, Ctrl+S` for Strategy.

### Fixed

- Reduced false errors on typed declarations and mixed-indentation files.
- "Open external website" dialog no longer appears when clicking CodeLens entries
- Removed Library template because it is not supported in this release.

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
  - Completion, hover and signature help work for user-defined functions with full parameter list.
  - Hover shows fields for User-Defined Types such as `type MySignal`.
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

- **Find All References** with Shift+F12 finds all usages of any user-defined symbol
- **Clickable Links** TradingView URLs in comments are now hyperlinks
- **Color Picker** inline color picker for `color.rgb` and all `color.*` constants
- **Format Document** normalizes indentation, trims trailing whitespace, collapses excess blank lines
- **Getting Started Walkthrough** 4-step onboarding in the VS Code Help tab
- Added new settings to control references, color tools, and formatting behavior.

## [0.5.0] 2026-06-05

### Added

- **Rename Symbol** with F2 renames any user-defined symbol across the file
- **Smart Folding** improves folding for script structures and long declarations.
- **Code Lens** shows usage count above every user-defined function
- **Pine Script Explorer** Activity Bar sidebar to browse all built-in namespaces and insert symbols

## [0.4.0] 2026-06-05

### Added

- **Real-time Diagnostics** for common Pine Script mistakes.
- **Go to Definition** with F12 jumps to user-defined symbols and opens TradingView docs for built-ins
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
