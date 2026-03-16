## csvchop — Standing Directive

A browser-side CSV inspector and JSON converter. Paste CSV, see a
formatted table, convert to JSON. Auto-detects delimiters. Nothing
leaves the browser.

### Current state

Single `index.html` (837 lines) with inlined CSS and JS. Uses
PapaParse for CSV parsing. Dark monospace theme. Functional but
has room for polish.

### Priority: Improve the tool

Work through these in order. Each one is a single commit.

1. **File drop support.** Add drag-and-drop to the textarea so users
   can drop a `.csv` file and have it parsed automatically. Show a
   visual drop zone indicator on dragover.

2. **Copy JSON to clipboard.** Add a "Copy" button next to the
   download button in the JSON view. Show brief "Copied!" feedback.

3. **Row count and column stats.** In the action bar, show total rows,
   total columns, and number of empty cells. Update live as the user
   types.

4. **Column type detection.** After parsing, detect column types
   (number, date, string, empty) and show a subtle type badge on
   each column header in the table view.

5. **TSV and pipe export.** Add export buttons for TSV and pipe-
   delimited output, not just JSON. Useful for users converting
   between formats.

6. **Keyboard shortcuts.** Cmd/Ctrl+Enter to parse, Cmd/Ctrl+Shift+C
   to copy JSON output, Cmd/Ctrl+K to clear. Show shortcuts in a
   small help tooltip.

### Rules

- Everything stays in one `index.html`. No build step, no npm.
- Preserve the existing design language (dark theme, monospace,
  gold accent).
- Test each change by pasting real CSV data before committing.
- Do not break existing functionality.
- Commit after each feature. Small, focused commits.
