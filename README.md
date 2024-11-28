# Tree(-sitter) of Knowledge

A collection of references, tips, and resources for working with and using Tree-sitter.

> [!WARNING]
> Spell it as Tree-sitter! Not treesitter, not tree sitter, not Tree Sitter, though I will accept tree-sitter. This is your first, only, and final warning!!!

## References & Resources

- [Homepage](https://tree-sitter.github.io/tree-sitter/)
- [Playground](https://tree-sitter.github.io/tree-sitter/playground)

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
- TODO: `:tree-sitter-subtree`.

#### Neovim

- The `:Inspect` command displays the current/active as well as overriden captures under the cursor, displayed in the colors of your theme, as a panel at the bottom of the editor.
- The `:InspectTree` command creates a new buffer (to the left) with the parsed syntax tree (like in the playground).

#### Zed

- The `debug: open syntax tree view` command opens a panel (to the right) with the parsed syntax tree (like in the playground, equivalent of Neovim's `:InspectTree` command). Is nicely colorful, supports clicking on nodes in the tree to move the cursor, and vice-versa (clicking around in the buffer updates the position / scrolls in the tree panel).
- The `editor: copy highlight json` command copies (a very large amount of) JSON to the clipboard; an array of arrays for each line, with each line's array containing objects for each highlighted token in the form of `{ text: string, highlight: string | null }` where `text` is the raw text content of the capture and `highlight` is the capture name.

## Other

### Articles

### Stats

- Editors using Tree-sitter: TBD
- Available grammars: TBD

### Editors using Tree-sitter

#### Active

- [Pulsar](https://pulsar-edit.dev/) (fork of Atom - see below)
- [Helix](https://helix-editor.com/)
- [Neovim](https://neovim.io/)
  - See also [nvim-treesitter/nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter).
- [Zed](https://zed.dev/)
- [Emacs](https://www.gnu.org/software/emacs/)* (as of [2022/11/22](https://lists.gnu.org/archive/html/emacs-devel/2022-11/msg01443.html), or Emacs 29+)
  - See also [emacs-tree-sitter](https://emacs-tree-sitter.github.io/).

##### Compatibility/Status

| Editor | Standard query precedence order | Standard injection captures | Language-scoped captures | Inheritable/extendable queries |
| --- | --- | --- | --- | --- |
| Zed | ✅ | 🚫<sup>[1](https://github.com/zed-industries/zed/issues/9656)</sup> | 🚫<sup>[1](https://github.com/zed-industries/zed/issues/9461#issuecomment-2480340039)</sup> | 🚫<sup>[1](https://github.com/zed-industries/zed/issues/8795)[2](https://github.com/zed-industries/zed/issues/16861)</sup> |
| Helix | 🚫 | ✅ | ✅ | ✅ |

#### Old

- [Atom](https://atom-editor.cc)
  - Sunset notice: https://github.blog/news-insights/product-news/sunsetting-atom/
  - Evidence: https://flight-manual.atom-editor.cc/hacking-atom/sections/creating-a-grammar/

### Projects using Tree-sitter (besides editors)

- [topiary](https://topiary.tweag.io/): formatting tool utilizing Tree-sitter; can use Tree-sitter queries to match nodes to certain defined capture types, such as `@prepend_space`, `@delete`, `@allow_blank_line_before`, etc.
