# Tree(-sitter) of Knowledge

A collection of references, tips, and resources for working with and using Tree-sitter.

> [!WARNING]
> Spell it as Tree-sitter! Not treesitter, not tree sitter, not Tree Sitter, though I will accept tree-sitter. This is your first, only, and final warning!!!

## References & Resources

- [Homepage](https://tree-sitter.github.io/tree-sitter/)
- [Playground](https://tree-sitter.github.io/tree-sitter/playground)

- [TS Questions](https://github.com/sogaiu/ts-questions/) - some tree-sitter-related questions with discussions and some answers.
  * [What Paths are Relevant for `tree-sitter` Use?](https://github.com/sogaiu/ts-questions/blob/master/questions/what-paths-are-relevant/README.md)
  * [What Files Are Involved in `tree-sitter generate`?](https://github.com/sogaiu/ts-questions/blob/master/questions/generate-subcommand-files/README.md)
  * [Should Generated Parser Source Be Committed?](https://github.com/sogaiu/ts-questions/blob/master/questions/should-parser-source-be-committed/README.md)
  * [What ABI Version Should Be Used for `parser.c`?](https://github.com/sogaiu/ts-questions/blob/master/questions/what-abi-level-should-be-used/README.md)
  * [Are External Scanners Commonly Used?](https://github.com/sogaiu/ts-questions/blob/master/questions/are-external-scanners-common/README.md)
  * [What Regular Expression Features Are Supported?](https://github.com/sogaiu/ts-questions/blob/master/questions/what-regex-features-are-supported/README.md)
  * [Which Version of Emscripten Should be Used for the Playground?](https://github.com/sogaiu/ts-questions/blob/master/questions/which-version-of-emscripten-should-be-used-for-the-playground/README.md)
  * [How Can a Custom Playground Be Hosted?](https://github.com/sogaiu/ts-questions/blob/master/questions/how-can-a-custom-playground-be-hosted/README.md)
  * [How Can One Test for An Expected Error?](https://github.com/sogaiu/ts-questions/blob/master/questions/how-to-test-for-an-expected-error/README.md)
  * [Is There Some Way to Influence Error Recovery?](https://github.com/sogaiu/ts-questions/blob/master/questions/is-there-some-way-to-influence-error-recovery/README.md)
  * [Is There A Changelog?](https://github.com/sogaiu/ts-questions/blob/master/questions/is-there-a-changelog/README.md)

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
- [Emacs](https://www.gnu.org/software/emacs/)* (as of [2022/11/22](https://lists.gnu.org/archive/html/emacs-devel/2022-11/msg01443.html), or Emacs 29+)
  - See also [emacs-tree-sitter](https://emacs-tree-sitter.github.io/).
- [Pulsar](https://pulsar-edit.dev/) (fork of Atom - see below)

##### Compatibility/Status

| Editor | Standard query precedence order | Standard injection captures | Language-scoped captures | Inheritable/extendable queries |
| --- | --- | --- | --- | --- |
| Neovim | ✅ | ✅ | ✅ | ✅ |
| Helix | 🚫 <sup>[1](https://github.com/helix-editor/helix/issues/9436) [2](https://github.com/uncenter/tree-sitter-query-reverser)</sup> | ✅ | ✅ | ✅ |
| Zed | ✅ | 🚫 <sup>[1](https://github.com/zed-industries/zed/issues/9656)</sup> | 🚫 <sup>[1](https://github.com/zed-industries/zed/issues/9461#issuecomment-2480340039)</sup> | 🚫 <sup>[1](https://github.com/zed-industries/zed/issues/8795) [2](https://github.com/zed-industries/zed/issues/16861)</sup> |
| Emacs | ? | ? | ? | ? |
| Pulsar | ? | ? | ? | ? |

#### Old (1)

- [Atom](https://atom-editor.cc)
  - Sunset notice: https://github.blog/news-insights/product-news/sunsetting-atom/
  - Evidence: https://flight-manual.atom-editor.cc/hacking-atom/sections/creating-a-grammar/

### Non-editor projects using Tree-sitter

- [topiary](https://topiary.tweag.io/): formatting tool utilizing Tree-sitter; can use Tree-sitter queries to match nodes to certain defined capture types, such as `@prepend_space`, `@delete`, `@allow_blank_line_before`, etc.
