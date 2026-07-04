# Pine Script DevKit for VS Code

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://github.com/SergeyChereshnyuk/vscode-extension-pinescript-feedback/blob/main/LICENSE)
[![VS Marketplace](https://img.shields.io/visual-studio-marketplace/v/chereshnyuk.chereshnyuk-com-pinescript?label=VS%20Marketplace)](https://marketplace.visualstudio.com/items?itemName=chereshnyuk.chereshnyuk-com-pinescript)
[![Installs](https://img.shields.io/visual-studio-marketplace/i/chereshnyuk.chereshnyuk-com-pinescript?label=Installs)](https://marketplace.visualstudio.com/items?itemName=chereshnyuk.chereshnyuk-com-pinescript)

**[Install from VS Marketplace](https://marketplace.visualstudio.com/items?itemName=chereshnyuk.chereshnyuk-com-pinescript)**

Pine Script v6 language support for Visual Studio Code with syntax highlighting, IntelliSense, hover docs, snippets, formatter, diagnostics, and `@pinescript` AI chat for TradingView.

Pine Script DevKit brings Pine Script development tools to VS Code for building TradingView indicators, strategies, and libraries. The extension provides language intelligence, documentation, diagnostics, navigation, formatting, templates, editor tooling, and GitHub Copilot integration in a single development experience. Create library scripts with the `library` snippet prefix; file templates are available for indicators and strategies.

---

## Code Intelligence

Pine Script DevKit includes complete Pine Script v6 language metadata sourced from the TradingView reference.

Namespace-aware autocomplete covers all built-in functions, variables, constants, and namespaces, along with your own functions, variables, types, and parameters. Hover tooltips and **signature help** provide inline documentation for both built-in and user-defined symbols at call sites.

Real-time diagnostics identify common Pine Script issues such as missing version declarations, incomplete indicator configuration, import resolution problems, and several common language pitfalls. Issues appear in the Problems panel with quick-fix code actions where applicable.

Semantic highlighting distinguishes user-defined functions, variables, types, and parameters from built-in language symbols.

---

## Navigation and Editing

Pine Script DevKit enhances the editing experience with syntax highlighting, navigation, formatting, and a range of editor integrations.

**Navigation:**

- **Symbol Navigation** — Go to Definition, **Go to Type Definition**, Find All References, and Rename Symbol
- **Workspace symbols** — Go to Symbol in Workspace (`Cmd+T` / `Ctrl+T`) for user-defined Pine symbols across open and saved `.pine` files (`pinescript.workspaceSymbols.enable`)
- **Document Outline** — functions, variables, UDTs, and inputs in breadcrumbs and the Outline panel
- **Code Lens** — usage count above every user-defined function
- **Smart Folding** — function bodies, `type` blocks, and `// #region` markers
- **Document Highlight** — all occurrences of the symbol under the cursor in real time
- **Document links** — clickable links on built-in call sites and field access (TradingView reference when enabled), the `//@version=6` header, and resolvable local import paths (not arbitrary URLs in comments or strings)

**Editing tools:**

- **40+ Snippets** — indicator, strategy, and library scaffolds, TA patterns, control flow, drawing objects, and tables
- **File Templates** — new Indicator or Strategy files via the Command Palette (**Pine Script: New Indicator** / **Pine Script: New Strategy**) or keyboard shortcuts
- **Inlay hints** — inferred types, effective overlay on `indicator()` / `strategy()` calls, and optional parameter names at call sites (`pinescript.inlayHints.enable`)
- **Inline completions** — opt-in Pine-specific ghost text for narrow patterns such as the version header (`pinescript.inlineCompletions.enable`, off by default to avoid overlapping Copilot)
- **Auto-Formatter** — document format, format selection, and on-type formatting; normalizes 4-space indentation, trims trailing whitespace, and collapses excess blank lines
- **Color Picker** — inline picker for `#RRGGBB`, `color.rgb()`, and all `color.*` named constants
- **Code Actions** — quick fixes to add `//@version=6`, add `overlay=`, or wrap a block with `barstate.isconfirmed`
- **Built-in discovery** — type `ta.`, `math.`, `strategy.`, or any namespace prefix to browse 200+ built-in functions with hover docs and signature help
- **Version diagnostics** — missing or non-v6 `//@version` declarations appear in the Problems panel; use the quick fix code action to add `//@version=6`
- **Reference links** — **View in Pine Script Reference** links in hover, completion details, and signature help open the official TradingView v6 page for built-in symbols (toggle with `pinescript.hover.showDocLinks`)

---

## Imports and Libraries

- **Library scaffolds** — use the `library` snippet prefix (there is no separate New Library file command)
- **Local imports** — `import` paths resolve via the workspace file system; Go to Definition and document links work on resolvable local targets
- **Virtual workspaces** — edit Pine in remote and virtual workspaces (for example [vscode.dev](https://vscode.dev) and GitHub Repositories) with diagnostics, IntelliSense, formatting, and local import support where workspace trust allows
- **Limitation** — workspace-wide reference search is not supported in virtual workspaces

---

## AI Integration

Pine Script DevKit includes a dedicated GitHub Copilot Chat participant and Copilot **Agent mode** Language Model Tools for Pine Script v6 development.

Use `@pinescript` in Copilot Chat to ask language-specific questions, explain code, generate Pine Script scaffolds, and get help while working in your project:

- `@pinescript how do I draw a horizontal line at the highest high of the last 20 bars?`
- `@pinescript /explain` — explain the selected Pine Script code
- `@pinescript /indicator` — generate an indicator scaffold
- `@pinescript /strategy` — generate a new strategy scaffold

**Agent mode tools** (enable in Copilot Agent mode when a `.pine` file is in context):

| Tool | Purpose |
|------|---------|
| `#lookupBuiltin` | Built-in signatures and docs from local metadata |
| `#getDiagnostics` | Current Pine diagnostics for the active editor |
| `#scaffold` | Indicator or strategy starter template (text only) |
| `#applyScaffold` | Write a scaffold to the workspace (requires folder + trust) |
| `#suggestFix` | Remediation hints for diagnostic codes |

Bundled **chat instructions**, **prompt files** (review, fix diagnostics, new indicator), and the **pine-indicator** skill attach automatically when a `.pine` file is in context.

**Workspace Trust:** `@pinescript` requires Workspace Trust. `#applyScaffold` requires trust and an open workspace folder. Core Pine language features (syntax, IntelliSense, diagnostics, formatting, navigation) remain available in Restricted Mode. Other Agent tools register without a trust gate but operate on editor context only.

AI-generated responses and code are provided as development assistance only. They may be incomplete, inaccurate, or unsuitable for your use case. Always review, test, and validate generated code in TradingView before relying on it.

Pine Script DevKit and its AI features do not provide investment advice, trading advice, or personalized financial recommendations.

---

## Platforms

| Environment | Support |
|-------------|---------|
| **VS Code desktop** | Full language features and Copilot integration |
| **VS Code for the web** | Web extension bundle; language features and AI when Copilot and trust allow |
| **Virtual workspaces** | Remote repos and vscode.dev; see [Imports and Libraries](#imports-and-libraries) for reference-search limits |
| **Restricted Mode** | Pine LSP features work; `@pinescript`, `#applyScaffold`, and workspace theme overrides require trust |

---

## Getting Started

1. [Install](https://marketplace.visualstudio.com/items?itemName=chereshnyuk.chereshnyuk-com-pinescript) the extension and open a `.pine` file.
2. Run **Help: Open Walkthrough…** and choose **Get Started with Pine Script** or **What's New in Pine Script DevKit 2.0**.
3. After updates, use **Pine Script: View Release Notes** from the Command Palette for bundled release notes.

**Deep links** (require a published extension version with the URI handler):

```text
vscode://chereshnyuk.chereshnyuk-com-pinescript/walkthrough/pinescript.gettingStarted
vscode://chereshnyuk.chereshnyuk-com-pinescript/settings/inlayHints.enable
vscode://chereshnyuk.chereshnyuk-com-pinescript/command/newIndicator
```

---

## Syntax Highlighting Colors

Pine Script DevKit automatically injects Pine Script syntax colors on top of your active VS Code theme. Colors adapt to light and dark mode automatically and only affect `.pine` files, leaving the rest of your editor untouched.

A custom `.pine` file icon is included and adapts to both light and dark editor themes.

---

## Commands and Shortcuts

| Action | How to run |
|--------|------------|
| **New Indicator** | Command Palette, Explorer context menu, `⌘⌥I` (macOS) / `Ctrl+Alt+I` (Windows/Linux), or [deep link](vscode://chereshnyuk.chereshnyuk-com-pinescript/command/newIndicator) |
| **New Strategy** | Command Palette, Explorer context menu, `⌘⌥S` / `Ctrl+Alt+S` |
| **Format Document** | Command Palette (**Pine Script: Format Document**), editor title run action, or `pinescript.formatDocument` |
| **View Release Notes** | Command Palette (**Pine Script: View Release Notes**) |
| **Go to Definition** | `F12` |
| **Go to Type Definition** | `Ctrl/Cmd+Click` or Command Palette |
| **Find All References** | `Shift+F12` |
| **Rename Symbol** | `F2` |
| **Go to Symbol in Workspace** | `Cmd+T` / `Ctrl+T` |

---

## Localization

Extension UI strings are localized for **14 VS Code display languages** (manifest `package.nls.*` and runtime `l10n/bundle.l10n.*`). VS Code picks the bundle matching your display language automatically.

---

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

---

## Requirements

- VS Code 1.125.0 or higher
- GitHub Copilot Chat for `@pinescript` and Agent mode tools

---

## Crash reporting (optional)

Pine Script DevKit can send **sanitized crash reports** to [Sentry](https://sentry.io) when you opt in. Crash reporting is **disabled by default**.

| Setting | Purpose |
|---|---|
| `pinescript.telemetry.sentry.enabled` | Opt in to crash reporting |
| `pinescript.telemetry.sentry.sampleRate` | Fraction of captured errors to send (0–1) |
| `pinescript.telemetry.sentry.environment` | Optional environment override |

Changes to these settings apply **immediately**; you do not need to reload the window.

**What may be sent**

- Extension error type and message (scrubbed)
- Extension version, VS Code version, platform, and Node.js version
- Stack traces from the extension bundle (`app:///` paths)
- Anonymous release-health session data (crash-free rate and error-rate per release)

**What is not sent**

- Pine script source code or open document text
- Auth tokens, cookies, or HTTP bodies
- Raw user file paths or `file://` URIs
- Performance traces, session replay, or profiling data

Reports are sent to Sentry's **EU ingest** region when enabled. This is opt-in stability telemetry (errors and release health), not usage analytics.

---

## Support and feedback

- **Questions:** [Marketplace Q&A](https://marketplace.visualstudio.com/items?itemName=chereshnyuk.chereshnyuk-com-pinescript)
- **Bugs and feature requests:** [GitHub Issues](https://github.com/SergeyChereshnyuk/vscode-extension-pinescript-feedback/issues)

---

## Extension Settings

All settings are available in the VS Code Settings editor under **Pine Script**.

### Diagnostics

| Setting | Purpose |
|---------|---------|
| `pinescript.diagnostics.enable` | Enable real-time Pine Script diagnostics |

### IntelliSense and navigation

| Setting | Purpose |
|---------|---------|
| `pinescript.hover.showDocLinks` | Show TradingView reference links in hover, completion, and signature help |
| `pinescript.completion.triggerOnDot` | Show namespace completions when typing a dot (for example `ta.`) |
| `pinescript.references.enable` | Enable Find All References for user-defined symbols |
| `pinescript.workspaceSymbols.enable` | Enable Go to Symbol in Workspace for user-defined Pine symbols |

### Editor

| Setting | Purpose |
|---------|---------|
| `pinescript.inlayHints.enable` | Master toggle for inlay hints |
| `pinescript.inlayHints.showInferredTypes` | Inferred series/simple qualifier hints on variables |
| `pinescript.inlayHints.showScriptOverlay` | Effective overlay flag on `indicator()` / `strategy()` calls |
| `pinescript.inlayHints.showParameterNames` | Parameter name hints at positional built-in call sites |
| `pinescript.inlineCompletions.enable` | Opt-in inline completions (off by default) |
| `pinescript.codeLens.enable` | Usage count above user-defined functions |
| `pinescript.color.enable` | Color picker for `color.rgb()` and `color.*` constants |
| `pinescript.formatting.enable` | Document, selection, and on-type formatting |

### Theme

| Setting | Purpose |
|---------|---------|
| `pinescript.theme.applyOverrides` | Opt-in workspace token color overrides (requires trust) |

### Telemetry

| Setting | Purpose |
|---------|---------|
| `pinescript.telemetry.sentry.enabled` | Opt-in Sentry crash reporting |
| `pinescript.telemetry.sentry.sampleRate` | Error sample rate when Sentry is enabled |
| `pinescript.telemetry.sentry.environment` | Optional Sentry environment override |

---

## Financial Disclaimer and Risk Notice

Pine Script DevKit is a software development tool for creating, reviewing and maintaining Pine Script code in Visual Studio Code.

It does not provide investment advice, trading advice, financial recommendations or personalized recommendations. Pine Script DevKit does not assess your financial circumstances, investment objectives, risk tolerance or the suitability of any financial instrument, trading strategy or transaction.

Diagnostics, code actions, documentation, GitHub Copilot integrations and generated code are provided for development and educational purposes only. They may be incomplete, inaccurate or unsuitable for your intended use.

You are solely responsible for reviewing, testing and validating any Pine Script code before relying on it. Any indicator, strategy or alert should be independently verified and appropriately backtested in TradingView before use in live or simulated trading.

Trading and investing involve risk, including the possible loss of capital. Past performance, backtesting results and hypothetical results do not guarantee future performance.

Pine Script DevKit is an independent project and is not affiliated with, endorsed by or sponsored by TradingView.

This extension is provided under the MIT License. The warranty disclaimer and limitation of liability in the `LICENSE` file apply to the maximum extent permitted by applicable law.
