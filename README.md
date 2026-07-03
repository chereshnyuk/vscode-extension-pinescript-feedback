# Pine Script DevKit for VS Code

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://github.com/SergeyChereshnyuk/vscode-extension-pinescript-feedback/blob/main/LICENSE)

Pine Script v6 language support for Visual Studio Code.

Pine Script DevKit brings Pine Script development tools to VS Code for building TradingView indicators, strategies and libraries. The extension provides language intelligence, documentation, diagnostics, navigation, formatting, templates, editor tooling and GitHub Copilot integration in a single development experience.

---

## Code Intelligence

Pine Script DevKit includes complete Pine Script v6 language metadata sourced from the TradingView reference.

Namespace-aware autocomplete covers all built-in functions, variables, constants, and namespaces, along with your own functions, variables, types, and parameters. Hover tooltips provide inline documentation for both built-in and user-defined symbols.

Real-time diagnostics identify common Pine Script issues such as missing version declarations, incomplete indicator configuration and several common language pitfalls.

Semantic highlighting distinguishes user-defined functions, variables, types and parameters from built-in language symbols.

---

## Editor Experience

Pine Script DevKit enhances the editing experience with syntax highlighting, navigation, formatting and a range of editor integrations.

**Navigation:**

- **Symbol Navigation** enables Go to Definition, Find All References and Rename Symbol.
- **Document Outline** shows functions, variables, UDTs and inputs in breadcrumbs and the Outline panel
- **Code Lens** shows usage count above every user-defined function
- **Smart Folding** for function bodies, `type` blocks and `// #region` markers
- **Document Highlight** highlights all occurrences of the symbol under cursor in real time

**Editing tools:**

- **25+ Snippets** covering indicator/strategy/library scaffolds, TA patterns, control flow, drawing objects and tables
- **File Templates** create new Indicator or Strategy files via the Command Palette (`Pine Script: New Indicator` / `Pine Script: New Strategy`) or keyboard shortcuts
- **Auto-Formatter** normalizes 4-space indentation, trims trailing whitespace and collapses excess blank lines
- **Color Picker** inline picker for `#RRGGBB`, `color.rgb()` and all `color.*` named constants
- **Code Actions** quick fixes to add `//@version=6`, add `overlay=`, or wrap a block with `barstate.isconfirmed`
- **Built-in discovery** Type `ta.`, `math.`, `strategy.`, or any namespace prefix to browse 200+ built-in functions with hover docs and signature help
- **Version diagnostics** Missing or non-v6 `//@version` declarations appear in the Problems panel; use the quick fix code action to add `//@version=6`
- **Reference links** **View in Pine Script Reference** links in hover, completion details, and signature help open the official TradingView v6 page for built-in symbols (toggle with `pinescript.hover.showDocLinks`)

---

## AI Integration

Pine Script DevKit includes a dedicated GitHub Copilot Chat participant for Pine Script v6 development.

Use `@pinescript` in Copilot Chat to ask language-specific questions, explain code, generate Pine Script scaffolds and get help while working in your project:

- `@pinescript how do I draw a horizontal line at the highest high of the last 20 bars?`
- `@pinescript /explain` - explain the selected Pine Script code
- `@pinescript /indicator` - generate an indicator scaffold
- `@pinescript /strategy` - generate a new strategy scaffold

AI-generated responses and code are provided as development assistance only. They may be incomplete, inaccurate or unsuitable for your use case. Always review, test and validate generated code in TradingView before relying on it.

Pine Script DevKit and its AI features do not provide investment advice, trading advice or personalized financial recommendations.

---

## Syntax Highlighting Colors

Pine Script DevKit automatically injects Pine Script syntax colors on top of your active VS Code theme. Colors adapt to light and dark mode automatically and only affect `.pine` files, leaving the rest of your editor untouched.

A custom `.pine` file icon is included and adapts to both light and dark editor themes.

---

## Commands and Shortcuts

Pine Script DevKit adds commands for creating new Pine Script files and supports standard VS Code navigation shortcuts.

- **New Indicator:** `⌘⌥I` on macOS, `Ctrl+Alt+I` on Windows and Linux  
- **New Strategy:** `⌘⌥S` on macOS, `Ctrl+Alt+S` on Windows and Linux  
- **Go to Definition:** `F12`  
- **Find All References:** `Shift+F12`  
- **Rename Symbol:** `F2`

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

- VS Code 1.125.0 or higher.
- GitHub Copilot Chat, for `@pinescript` AI features.

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

Pine Script DevKit provides configurable options for diagnostics, IntelliSense, documentation, formatting and editor integrations. All settings are available through the standard VS Code Settings editor.

---

## Financial Disclaimer and Risk Notice

Pine Script DevKit is a software development tool for creating, reviewing and maintaining Pine Script code in Visual Studio Code.

It does not provide investment advice, trading advice, financial recommendations or personalized recommendations. Pine Script DevKit does not assess your financial circumstances, investment objectives, risk tolerance or the suitability of any financial instrument, trading strategy or transaction.

Diagnostics, code actions, documentation, GitHub Copilot integrations and generated code are provided for development and educational purposes only. They may be incomplete, inaccurate or unsuitable for your intended use.

You are solely responsible for reviewing, testing and validating any Pine Script code before relying on it. Any indicator, strategy or alert should be independently verified and appropriately backtested in TradingView before use in live or simulated trading.

Trading and investing involve risk, including the possible loss of capital. Past performance, backtesting results and hypothetical results do not guarantee future performance.

Pine Script DevKit is an independent project and is not affiliated with, endorsed by or sponsored by TradingView.

This extension is provided under the MIT License. The warranty disclaimer and limitation of liability in the `LICENSE` file apply to the maximum extent permitted by applicable law.