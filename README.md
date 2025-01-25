# Tree(-sitter) of Knowledge

A collection of references, tips, and resources for working with and using Tree-sitter.

> [!WARNING]
> Spell it as Tree-sitter! Not treesitter, not tree sitter, not Tree Sitter, though I will accept tree-sitter. This is your first, only, and final warning!!!

## References & Resources

- [Homepage](https://tree-sitter.github.io/tree-sitter/)
- [Playground](https://tree-sitter.github.io/tree-sitter/playground)

- [TS Questions](https://github.com/sogaiu/ts-questions/) - some tree-sitter-related questions with discussions and some answers.
  - [What Paths are Relevant for `tree-sitter` Use?](https://github.com/sogaiu/ts-questions/blob/master/questions/what-paths-are-relevant/README.md)
  - [What Files Are Involved in `tree-sitter generate`?](https://github.com/sogaiu/ts-questions/blob/master/questions/generate-subcommand-files/README.md)
  - [Should Generated Parser Source Be Committed?](https://github.com/sogaiu/ts-questions/blob/master/questions/should-parser-source-be-committed/README.md)
  - [What ABI Version Should Be Used for `parser.c`?](https://github.com/sogaiu/ts-questions/blob/master/questions/what-abi-level-should-be-used/README.md)
  - [Are External Scanners Commonly Used?](https://github.com/sogaiu/ts-questions/blob/master/questions/are-external-scanners-common/README.md)
  - [What Regular Expression Features Are Supported?](https://github.com/sogaiu/ts-questions/blob/master/questions/what-regex-features-are-supported/README.md)
  - [Which Version of Emscripten Should be Used for the Playground?](https://github.com/sogaiu/ts-questions/blob/master/questions/which-version-of-emscripten-should-be-used-for-the-playground/README.md)
  - [How Can a Custom Playground Be Hosted?](https://github.com/sogaiu/ts-questions/blob/master/questions/how-can-a-custom-playground-be-hosted/README.md)
  - [How Can One Test for An Expected Error?](https://github.com/sogaiu/ts-questions/blob/master/questions/how-to-test-for-an-expected-error/README.md)
  - [Is There Some Way to Influence Error Recovery?](https://github.com/sogaiu/ts-questions/blob/master/questions/is-there-some-way-to-influence-error-recovery/README.md)
  - [Is There A Changelog?](https://github.com/sogaiu/ts-questions/blob/master/questions/is-there-a-changelog/README.md)
- [Tips and tricks for a grammar author](https://github.com/tree-sitter/tree-sitter/wiki/Tips-and-Tricks-for-a-grammar-author)
  - Reducing state count
  - External scanner building & debugging
    - When/how to use mark_end
- [Grammar Development for Semantic Code](https://github.com/github/semantic/blob/main/docs/grammar-development-guide.md)
  - Rely on Language Specs, but not too much
  - Study and test with other language parsers
  - Think through use-cases for parse trees
  - Know when to parse invalid syntax
  - What does a "good" parse tree look like?
  - Improving a parse tree
  - Making your tree compact: knowing when to inline vs. hide vs. remove a rule
  - Test in the wild to prioritize what's next
  - Sequence your work
  - Handling conflicts
  - Debugging errors

### Editor Captures

- Documentation?: https://tree-sitter.github.io/tree-sitter/syntax-highlighting#theme

- Neovim: https://neovim.io/doc/user/treesitter.html#treesitter-highlight-groups.
- Helix: https://docs.helix-editor.com/themes.html#scopes
- Zed: https://zed.dev/docs/extensions/languages#syntax-highlighting

## Tips

### Debugging

#### Helix

- The `:tree-sitter-scopes` command displays a tooltip over the cursor with an array of node names, in order of the AST's depth (e.g. `["program", "expression_statement", ...]`).
- The `:tree-sitter-highlight-name` command displays a tooltip over the cursor with the name of the currently active capture.
- The `:tree-sitter-subtree` command displays a tooltip over the selection containing the smallest possible subtree that covers all selected nodes.

#### Neovim

- The `:Inspect` command displays the current/active as well as overriden captures under the cursor, displayed in the colors of your theme, as a panel at the bottom of the editor.
- The `:InspectTree` command creates a new buffer (to the left) with the parsed syntax tree (like in the playground).

#### Zed

- The `debug: open syntax tree view` command opens a panel (to the right) with the parsed syntax tree (like in the playground, equivalent of Neovim's `:InspectTree` command). Is nicely colorful, supports clicking on nodes in the tree to move the cursor, and vice-versa (clicking around in the buffer updates the position / scrolls in the tree panel).
- The `editor: copy highlight json` command copies (a very large amount of) JSON to the clipboard; an array of arrays for each line, with each line's array containing objects for each highlighted token in the form of `{ text: string, highlight: string | null }` where `text` is the raw text content of the capture and `highlight` is the capture name.

## Other

### Articles

TODO

### Editors using Tree-sitter (6)

- [Visual Studio Code support for Tree-sitter?](https://github.com/microsoft/vscode/issues/50140)

#### Active (5)

- [Neovim](https://neovim.io/)
  - See also [nvim-treesitter/nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter).
- [Helix](https://helix-editor.com/)
- [Zed](https://zed.dev/)
- [Emacs](https://www.gnu.org/software/emacs/)\* (as of [2022/11/22](https://lists.gnu.org/archive/html/emacs-devel/2022-11/msg01443.html), or Emacs 29+)
  - See also [emacs-tree-sitter](https://emacs-tree-sitter.github.io/).
- [Pulsar](https://pulsar-edit.dev/) (fork of Atom - see below)

##### Compatibility/Status

| Editor | Standard query precedence order | Language-scoped captures | Inheritable/extendable queries |
| ------ | ------------------------------- | ------------------------ | ------------------------------ |
| Neovim | ✅                              | ✅                       | ✅                             |
| Helix  | 🚫 [^1][^2]                     | ✅                       | ✅                             |
| Zed    | ✅                              | 🚫 [^3]                  | 🚫 [^4][^5]                    |
| Emacs  | ?                               | ?                        | ?                              |
| Pulsar | ?                               | ?                        | ?                              |

#### Old (1)

- [Atom](https://atom-editor.cc)
  - Sunset notice: https://github.blog/news-insights/product-news/sunsetting-atom/
  - Evidence: https://flight-manual.atom-editor.cc/hacking-atom/sections/creating-a-grammar/

### Non-editor projects using Tree-sitter

- [topiary](https://topiary.tweag.io/): formatting tool utilizing Tree-sitter; can use Tree-sitter queries to match nodes to certain defined capture types, such as `@prepend_space`, `@delete`, `@allow_blank_line_before`, etc.
- [ast-grep](https://ast-grep.github.io/): a fast and polyglot tool for code structural search, lint, rewriting at large scale.

[^1]: [Reverse tree-sitter query precedence ordering · Issue #9436 · helix-editor/helix](https://github.com/helix-editor/helix/issues/9436)
[^2]: [uncenter/tree-sitter-query-reverser: ⏪ Literally reverse the order of Tree-sitter queries to better work with Helix.](https://github.com/uncenter/tree-sitter-query-reverser)
[^3]: [Support more syntax tokens for theme configuration · Issue #9461 · zed-industries/zed](https://github.com/zed-industries/zed/issues/9461#issuecomment-2480340039)
[^4]: [merge registered language with existing language, so languages can be extended · Issue #8795 · zed-industries/zed](https://github.com/zed-industries/zed/issues/8795)
[^5]: [Extension API for extending language queries · Issue #16861 · zed-industries/zed](https://github.com/zed-industries/zed/issues/16861)
