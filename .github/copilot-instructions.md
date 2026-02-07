# Copilot instructions for Against-all-odds_C1

Purpose
- Provide repo-specific guidance for GitHub Copilot CLI sessions working with this project.

Build, test, and lint
- This repository is a single-file Twine (Harlowe) export: index.html. There are no build, test, or lint scripts.
- To run locally (static):
  - Open index.html directly in a browser, or serve it from the project directory:
    - python3 -m http.server 8000  (then open http://localhost:8000/Against-all-odds_C1/)
  - Manual test: open the browser DevTools console and click a story choice; the page logs "USER CLICKED: ..." and posts a message { type: 'twine-click', choice } to window.parent.

High-level architecture
- Single static HTML export produced by Twine (Harlowe). The runtime is fully contained in index.html.
- Key runtime elements inside index.html:
  - <tw-storydata ... ifid="..." startnode="..."> contains all passages as <tw-passagedata> entries.
  - <tw-story>, <tw-passagedata>, and custom <tw-link> elements represent story structure and choices.
  - The Twine engine and runtime scripts are embedded in the file (minified/packaged code).
  - A small tracking script (in a passage named "Tracking" and repeated near the end) listens for clicks on <tw-link> and forwards choices via window.parent.postMessage with type 'twine-click'.

Key conventions and cautions
- Passage naming: many passages use names like "C1-...", "Choice_X", "Merge_..."; search for tw-passagedata names when locating content.
- Preserve the story IFID: the tw-storydata ifid attribute is used for analytics; avoid changing it unless intentional.
- Prefer editing via the Twine editor and re-exporting the HTML rather than hand-editing the embedded engine code.
- If editing index.html by hand, only modify:
  - the contents of <tw-passagedata> (passage text),
  - the twine-user-stylesheet (id="twine-user-stylesheet"),
  - the twine-user-script (id="twine-user-script").
  Do NOT remove or alter the embedded Twine engine script block or the tw-storydata attributes unless you know the consequences.
- Tracking: keep the window.parent.postMessage payload and the console logging intact if downstream systems (Qualtrics, parent frames) depend on them.
- Search shortcuts for automation or copilot prompts: use the tokens `tw-passagedata`, `tw-link`, `tw-storydata`, and `ifid` when searching the file to find story content and analytics hooks.

Existing docs and AI assistant configs
- No README.md, CONTRIBUTING.md, or recognized AI assistant config files (CLAUDE.md, AGENTS.md, .cursorrules, .windsurfrules, etc.) were found in the repository root. Consider adding the Twine source (.tws) or a README to simplify edits and CI.

Suggested minimal repo improvements (optional)
- Add the original Twine project file (.tws) or a short README describing editing/export workflow.
- Add a simple package.json or Makefile only if automated checks or CI are needed.

MCP servers
- Would you like to configure any MCP servers related to this project (for example, Playwright for automated browser-based tests)?

If you want changes
- I created .github/copilot-instructions.md with the guidance above. Tell me if you want this expanded, adjusted, or if you want automated test instructions added.

