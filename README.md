# Pine Script DevKit for VS Code

Pine Script v6 language support for Visual Studio Code with syntax highlighting, IntelliSense, hover docs, snippets, formatter, diagnostics, and `@pinescript` AI chat for TradingView.

Pine Script DevKit brings Pine Script development tools to VS Code for building TradingView indicators, strategies, and libraries. The extension provides language intelligence, documentation, diagnostics, navigation, formatting, templates, editor tooling, and GitHub Copilot integration in a single development experience. Create library scripts with the `library` snippet prefix; file templates are available for indicators and strategies.

## Code Intelligence

Pine Script DevKit includes complete Pine Script v6 language metadata sourced from the TradingView reference.

Namespace-aware autocomplete covers all built-in functions, variables, constants, and namespaces, along with your own functions, variables, types, and parameters. Hover tooltips and **signature help** provide inline documentation for both built-in and user-defined symbols at call sites.

Real-time diagnostics identify common Pine Script issues such as missing version declarations, incomplete indicator configuration, import resolution problems, and several common language pitfalls. Issues appear in the Problems panel with quick-fix code actions where applicable.

Semantic highlighting distinguishes user-defined functions, variables, types, and parameters from built-in language symbols.

## AI Integration

Pine Script DevKit includes a dedicated GitHub Copilot Chat participant and Copilot **Agent mode** Language Model Tools for Pine Script v6 development.

Use `@pinescript` in Copilot Chat to ask language-specific questions, explain code, generate Pine Script scaffolds, and get help while working in your project:

- **`@pinescript how do I draw a horizontal line at the highest high of the last 20 bars?`**
- **`@pinescript /explain`**: explain the selected Pine Script code
- **`@pinescript /indicator`**: generate an indicator scaffold
- **`@pinescript /strategy`**: generate a new strategy scaffold

Enable **Agent mode tools** in Copilot Agent mode when a `.pine` file is in context:

- **`#lookupBuiltin`**: built-in signatures and docs from local metadata
- **`#getDiagnostics`**: current Pine diagnostics for the active editor
- **`#scaffold`**: indicator or strategy starter template, text only
- **`#applyScaffold`**: write a scaffold to the workspace; requires an open folder and Workspace Trust
- **`#suggestFix`**: remediation hints for diagnostic codes

Bundled **chat instructions**, **prompt files** for review, diagnostic fixes, and new indicators, and the **pine-indicator** skill attach automatically when a `.pine` file is in context.

**Workspace Trust:** `@pinescript` requires Workspace Trust. `#applyScaffold` requires trust and an open workspace folder. Core Pine language features including syntax, IntelliSense, diagnostics, formatting, and navigation remain available in Restricted Mode. Other Agent tools register without a trust gate but operate on editor context only.

AI-generated responses and code are provided as development assistance only. They may be incomplete, inaccurate, or unsuitable for your use case. Always review, test, and validate generated code in TradingView before relying on it.

Pine Script DevKit and its AI features do not provide investment advice, trading advice, or personalized financial recommendations.

## Marketplace FEATURES Reference

The VS Code Marketplace **FEATURES** tab lists technical contributions declared in the extension manifest. Use this map when reviewing the listing in Extension Details:

- **Runtime Status**: activation timing and workspace capability flags such as virtual workspaces and Restricted Mode behavior.
- **Activation Events**: when Pine Script DevKit loads: opening a workspace folder that contains `.pine` files, opening a `.pine` file, running Pine commands, starting walkthroughs, invoking `@pinescript`, or calling Agent Language Model Tools.
- **Chat Instructions**: bundled Pine Script v6 guidelines Copilot applies when a `.pine` file is in context.
- **Chat Participants**: the `@pinescript` Copilot Chat participant for explain, indicator, and strategy workflows.
- **Chat Prompt Files**: reusable slash prompts for review, diagnostic fixes, and new indicators.
- **Chat Skills**: the **pine-indicator** Agent skill for scaffold and debug workflows.
- **Commands**: **Pine Script: New Indicator**, **New Strategy**, **Format Document**, and **View Release Notes**.
- **Language Model Tools**: `#lookupBuiltin`, `#getDiagnostics`, `#scaffold`, `#applyScaffold`, and `#suggestFix` for Agent mode.
- **Programming Languages**: Pine Script grammar, `.pine` file association, snippets, and semantic token types.
- **Settings**: every `pinescript.*` configuration key documented in [Extension Settings](#extension-settings).
- **Settings Default Overrides**: Pine-scoped syntax and semantic colors applied only to `.pine` files; stronger workspace theme writes require `pinescript.theme.applyOverrides`.

## Navigation

Move through Pine scripts and workspace symbols with definition, reference, and outline tooling.

- **Symbol Navigation**: Go to Definition, **Go to Type Definition**, Find All References, and Rename Symbol
- **Workspace symbols**: Go to Symbol in Workspace with `Cmd+T` on macOS or `Ctrl+T` on Windows and Linux for user-defined Pine symbols across open and saved `.pine` files; toggle with `pinescript.workspaceSymbols.enable`
- **Document Outline**: functions, variables, UDTs, and inputs in breadcrumbs and the Outline panel
- **Code Lens**: usage count above every user-defined function
- **Smart Folding**: function bodies, `type` blocks, and `// #region` markers
- **Document Highlight**: all occurrences of the symbol under the cursor in real time
- **Document links**: clickable links on built-in call sites and field access when TradingView reference links are enabled, the `//@version=6` header, and resolvable local import paths; arbitrary URLs in comments or strings are not linked

## Editing

Format, scaffold, and refine Pine scripts with snippets, templates, inlay hints, and editor integrations.

- **40+ Snippets**: indicator, strategy, and library scaffolds, TA patterns, control flow, drawing objects, and tables
- **File Templates**: new Indicator or Strategy files via the Command Palette with **Pine Script: New Indicator** or **Pine Script: New Strategy**, or keyboard shortcuts
- **Inlay hints**: inferred types, effective overlay on `indicator()` / `strategy()` calls, and optional parameter names at call sites; toggle with `pinescript.inlayHints.enable`
- **Inline completions**: opt-in Pine-specific ghost text for narrow patterns such as the version header; toggle with `pinescript.inlineCompletions.enable`, off by default to avoid overlapping Copilot
- **Auto-Formatter**: document format, format selection, and on-type formatting; normalizes 4-space indentation, trims trailing whitespace, and collapses excess blank lines
- **Color Picker**: inline picker for `#RRGGBB`, `color.rgb()`, and all `color.*` named constants
- **Code Actions**: quick fixes to add `//@version=6`, add `overlay=`, or wrap a block with `barstate.isconfirmed`
- **Built-in discovery**: type `ta.`, `math.`, `strategy.`, or any namespace prefix to browse 200+ built-in functions with hover docs and signature help
- **Version diagnostics**: missing or non-v6 `//@version` declarations appear in the Problems panel; use the quick fix code action to add `//@version=6`
- **Reference links**: **View in Pine Script Reference** links in hover, completion details, and signature help open the official TradingView v6 page for built-in symbols; toggle with `pinescript.hover.showDocLinks`

## Imports and Libraries

- **Library scaffolds**: use the `library` snippet prefix; there is no separate New Library file command
- **Local imports**: `import` paths resolve via the workspace file system; Go to Definition and document links work on resolvable local targets
- **Virtual workspaces**: edit Pine in remote and virtual workspaces such as [vscode.dev](https://vscode.dev) and GitHub Repositories with diagnostics, IntelliSense, formatting, and local import support where workspace trust allows
- **Limitation**: workspace-wide reference search is not supported in virtual workspaces

## Platforms

- **VS Code desktop**: full language features and Copilot integration
- **VS Code for the web**: web extension bundle; language features and AI when Copilot and trust allow
- **Virtual workspaces**: remote repos and vscode.dev; see [Imports and Libraries](#imports-and-libraries) for reference-search limits
- **Restricted Mode**: Pine LSP features work; `@pinescript`, `#applyScaffold`, and workspace theme overrides require trust

## Getting Started

1. [Install](https://marketplace.visualstudio.com/items?itemName=chereshnyuk.chereshnyuk-com-pinescript) the extension and open a folder that contains Pine Script files or open a `.pine` file directly.
2. Run **Help: Open Walkthrough…** and choose **Get Started with Pine Script** or **What's New in Pine Script DevKit 2.0**.
3. After updates, use **Pine Script: View Release Notes** from the Command Palette for bundled release notes.

## Syntax Highlighting Colors

Pine Script DevKit automatically injects Pine Script syntax colors on top of your active VS Code theme. Colors adapt to light and dark mode automatically and only affect `.pine` files, leaving the rest of your editor untouched.

A custom `.pine` file icon is included and adapts to both light and dark editor themes.

## Commands and Shortcuts

- **New Indicator**: Command Palette, Explorer context menu, `⌘⌥I` on macOS, `Ctrl+Alt+I` on Windows and Linux, or [deep link](vscode://chereshnyuk.chereshnyuk-com-pinescript/command/newIndicator)
- **New Strategy**: Command Palette, Explorer context menu, `⌘⌥S` on macOS, `Ctrl+Alt+S` on Windows and Linux
- **Format Document**: Command Palette with **Pine Script: Format Document**, `Shift+Alt+F` when a `.pine` file is focused, or `pinescript.formatDocument`
- **View Release Notes**: Command Palette with **Pine Script: View Release Notes**
- **Go to Definition**: `F12`
- **Go to Type Definition**: `Ctrl/Cmd+Click` or Command Palette
- **Find All References**: `Shift+F12`
- **Rename Symbol**: `F2`
- **Go to Symbol in Workspace**: `Cmd+T` on macOS or `Ctrl+T` on Windows and Linux

## Localization

The extension UI is localized for 14 VS Code display languages. VS Code automatically selects the matching language bundle when available.

## Support the Project

Pine Script DevKit is maintained independently. If it helps your Pine Script workflow, you can support its development.
<p align="center">
  <a href="https://buymeacoffee.com/chereshnyuk">
    <img src="assets/buy-me-a-coffee-qr.png" width="220" alt="Support Pine Script DevKit on Buy Me a Coffee" />
  </a>
</p>
<p align="center">
  <a href="https://buymeacoffee.com/chereshnyuk">Buy me a coffee</a>
</p>

## Requirements

- VS Code 1.125.0 or higher
- GitHub Copilot Chat for `@pinescript` and Agent mode tools

## Crash reporting

When **VS Code telemetry** is enabled and `telemetry.telemetryLevel` is not `off`, Pine Script DevKit can send **sanitized crash reports** to [Sentry](https://sentry.io) EU ingest. Data goes to the extension author's Sentry project, not to Microsoft.

- **`telemetry.telemetryLevel`**: VS Code setting that controls whether crash and error telemetry may be sent
- **`pinescript.telemetry.sentry.sampleRate`**: fraction of captured errors to send from 0 to 1
- **`pinescript.telemetry.sentry.environment`**: optional Sentry environment override

Changes to the Pine Script Sentry settings apply **immediately**; you do not need to reload the window.

**What may be sent**
- Extension error type and message with sensitive details removed
- Extension version, VS Code version, platform, and Node.js version
- Stack traces from the extension bundle with `app:///` paths
- Anonymous release-health session data for crash-free rate and error-rate per release, not install counts

**What is not sent**
- Install or first-run events
- Pine script source code or open document text
- Auth tokens, cookies, or HTTP bodies
- Raw user file paths or `file://` URIs
- Performance traces, session replay, profiling, or usage analytics

## Support and feedback

- **Questions:** [Marketplace Q&A](https://marketplace.visualstudio.com/items?itemName=chereshnyuk.chereshnyuk-com-pinescript)
- **Bugs and feature requests:** [GitHub Issues](https://github.com/chereshnyuk/vscode-extension-pinescript-feedback/issues)

## Extension Settings

All settings are available in the VS Code Settings editor under **Pine Script**.
- **`pinescript.diagnostics.enable`**: enable real-time Pine Script diagnostics
- **`pinescript.hover.showDocLinks`**: show TradingView reference links in hover, completion, and signature help
- **`pinescript.completion.triggerOnDot`**: show namespace completions when typing a dot such as `ta.`
- **`pinescript.references.enable`**: enable Find All References for user-defined symbols
- **`pinescript.workspaceSymbols.enable`**: enable Go to Symbol in Workspace for user-defined Pine symbols
- **`pinescript.inlayHints.enable`**: master toggle for inlay hints
- **`pinescript.inlayHints.showInferredTypes`**: inferred series/simple qualifier hints on variables
- **`pinescript.inlayHints.showScriptOverlay`**: effective overlay flag on `indicator()` / `strategy()` calls
- **`pinescript.inlayHints.showParameterNames`**: parameter name hints at positional built-in call sites
- **`pinescript.inlineCompletions.enable`**: opt-in inline completions; off by default
- **`pinescript.codeLens.enable`**: usage count above user-defined functions
- **`pinescript.color.enable`**: color picker for `color.rgb()` and `color.*` constants
- **`pinescript.formatting.enable`**: document, selection, and on-type formatting
- **`pinescript.theme.applyOverrides`**: opt-in workspace token color overrides; requires Workspace Trust
- **`pinescript.telemetry.sentry.sampleRate`**: error sample rate when VS Code telemetry allows Sentry reporting
- **`pinescript.telemetry.sentry.environment`**: optional Sentry environment override

## Financial Disclaimer and Risk Notice

Pine Script DevKit is a software development tool for creating, reviewing and maintaining Pine Script code in Visual Studio Code.

It does not provide investment advice, trading advice, financial recommendations or personalized recommendations. Pine Script DevKit does not assess your financial circumstances, investment objectives, risk tolerance or the suitability of any financial instrument, trading strategy or transaction.

Diagnostics, code actions, documentation, GitHub Copilot integrations and generated code are provided for development and educational purposes only. They may be incomplete, inaccurate or unsuitable for your intended use.

You are solely responsible for reviewing, testing and validating any Pine Script code before relying on it. Any indicator, strategy or alert should be independently verified and appropriately backtested in TradingView before use in live or simulated trading.

Trading and investing involve risk, including the possible loss of capital. Past performance, backtesting results and hypothetical results do not guarantee future performance.

Pine Script DevKit is an independent project and is not affiliated with, endorsed by or sponsored by TradingView.

This extension is provided under the MIT License. The warranty disclaimer and limitation of liability in the `LICENSE` file apply to the maximum extent permitted by applicable law.