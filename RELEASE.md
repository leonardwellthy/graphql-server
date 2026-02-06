Release type: patch

Fix GraphiQL IDE rendering issues introduced in v3.0.0:

- Fix Flask views using Jinja2's `render_template_string` which
  HTML-escaped JSON values (e.g., `&#34;` instead of `"`), breaking
  the GraphiQL JavaScript configuration. Both sync and async Flask
  views now use `to_template_string()` with the framework-agnostic
  `simple_renderer`.
- Fix `operationName` not being passed to the GraphiQL template due
  to a variable naming mismatch (`operationName` vs `operation_name`)
  in the sync Flask view.
- Restore the `locationQuery` JavaScript function that was
  accidentally removed, which caused a `ReferenceError` when editing
  queries, variables, or headers in the GraphiQL IDE.
- Escape `<` and `>` as `\u003c` and `\u003e` in `tojson()` to
  prevent queries containing `</script>` from breaking the GraphiQL
  page by prematurely closing the script tag.
- Add CodeMirror 5 fold gutter CSS to fix missing/broken fold
  markers in the GraphiQL editor.
