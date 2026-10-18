# MathPoint — TeX math in PowerPoint and Word from Claude or ChatGPT

MathPoint is an add-in for Microsoft PowerPoint and Word. Ask Claude or ChatGPT
in chat, and equations, TikZ / pgfplots figures, and tables typeset with TeX
appear in the slide deck or document you have open. Typesetting runs on the
MathPoint server with LuaLaTeX, so you do not need TeX installed.

![A PowerPoint slide with a TeX-typeset 3D plot of a bivariate Gaussian and its density formula, next to the MathPoint task pane listing what Claude did](assets/screenshot.png)

- **Product page:** <https://tex64.com/mathpoint> (日本語: <https://tex64.com/ja/mathpoint>)
- **Guide:** <https://mcp.tex64.com/mathpoint/docs>
- **MCP server:** `https://mcp.tex64.com/mathpoint/mcp` (Streamable HTTP, OAuth sign-in with Google)

This repository holds the public connection details: the Claude plugin, the MCP
Registry entry, and this README. The MathPoint service itself is operated by
Fermion Inc.

## Get started

1. **Install the add-in** (PowerPoint and Word, Microsoft 365 or Office 2021 and later):

   ```sh
   # Mac (Terminal)
   curl -fsSL https://mcp.tex64.com/mathpoint/install | sh
   ```

   ```powershell
   # Windows (PowerShell)
   irm https://mcp.tex64.com/mathpoint/install.ps1 | iex
   ```

   On the web, use Add-ins → More Add-ins → My Add-ins → Upload My Add-in and
   choose [manifest.prod.xml](https://mcp.tex64.com/mathpoint/addin/manifest.prod.xml).

2. **Sign in.** Reopen PowerPoint or Word, open **Home → Add-ins → MathPoint**,
   and sign in with Google in the task pane.

3. **Connect your AI.** Choose Claude or ChatGPT in the task pane, or add the
   MCP server yourself:

   | Client | How |
   |---|---|
   | Claude (claude.ai, desktop) | Settings → Connectors → Add custom connector → `https://mcp.tex64.com/mathpoint/mcp` |
   | ChatGPT | Settings → Apps & Connectors → create a connector (developer mode) with the same URL |
   | Claude Code | `claude mcp add --transport http mathpoint https://mcp.tex64.com/mathpoint/mcp`, or install this plugin: `/plugin marketplace add Fermion-company/mathpoint-plugin` then `/plugin install mathpoint@mathpoint` |
   | Codex | `codex mcp add mathpoint --url https://mcp.tex64.com/mathpoint/mcp` |

4. **Ask.** Keep the task pane open and ask in chat.

## Example prompts

- “Put the quadratic formula on slide 2.”
- “Make the equations on slide 2 teal and a bit larger.”
- “Add a slide with a 3D surface plot of a bivariate Gaussian.”
- “Redraw this hand-drawn circuit as a clean figure and put it on slide 3.”
- “Turn this table into a booktabs-style table with the decimals aligned.”
- “In my Word document, add Euler’s identity after paragraph 3, and make a ≠ 0 in the text inline math.”
- “Typeset Maxwell’s equations and show me the image.” (works without Office)

## Tools

| Tool | What it does | Annotation |
|---|---|---|
| `list_slides`, `list_layouts`, `word_read` | Read slides, layouts, and Word paragraphs | read-only |
| `insert_math`, `word_insert_math` | Typeset LaTeX with TeX and insert it (display, inline, or text mode) | write |
| `update_math`, `word_update_math` | Re-typeset a MathPoint shape with new LaTeX, size, or color | write, replaces |
| `render_math` | Return typeset math as a PNG without touching any file | read-only |
| `figure_guide`, `figure_start`, `figure_requests`, `figure_build`, `figure_place`, … | Build TikZ / pgfplots figures and tabularray tables, including redraws of sketches and screenshots, then place them | write |
| `set_text`, `add_text_box`, `add_slide`, `move_shape`, `delete_shape` | Edit ordinary PowerPoint text and layout | write |
| `word_insert_text`, `word_set_text`, `word_delete` | Edit Word paragraphs | write |
| `insert_image`, `word_insert_image` | Place an image as it is | write |
| `select_file`, `usage` | Choose which open file to edit; this month’s usage | — |

Edits appear in the open file right away and can be undone with Undo.

## Plans

The free plan covers 30 typeset equations, figures, or tables a month
(re-typesetting the same item does not count again). A paid plan without a
monthly limit (600 JPY a month, tax included) is on the way.

## Privacy

Full policy: <https://mcp.tex64.com/mathpoint/privacy>. In short:

- MathPoint can edit only files where the MathPoint task pane is open.
- Slide and document content passes through the server only when your AI reads
  it; it is not stored.
- TeX sources and typeset results are kept for up to 30 days for your work.
- Sign-in uses Google. You can disconnect AI apps or delete your account at any
  time from <https://mcp.tex64.com/mathpoint/account>.

## 日本語

MathPoint は PowerPoint と Word のアドインです。Claude や ChatGPT にチャットで
頼むと、開いているスライドや文書に TeX で組んだ数式・図・表が入ります。組版は
サーバーで行うので、TeX のインストールは要りません。

1. Mac はターミナルで `curl -fsSL https://mcp.tex64.com/mathpoint/install | sh`、
   Windows は PowerShell で `irm https://mcp.tex64.com/mathpoint/install.ps1 | iex` を実行します。
2. PowerPoint を開き直し、ホーム → アドイン → MathPoint を開いて Google でログインします。
3. 作業ウィンドウから Claude か ChatGPT をつなぎ、「スライド 2 に二次方程式の解の公式を入れて」のように頼みます。

無料プランは月 30 件までです。詳しくは <https://tex64.com/ja/mathpoint> をご覧ください。

## Support

<contact@fermion.company> · <https://mcp.tex64.com/mathpoint/support>

## License

The files in this repository are MIT licensed. The MathPoint service is subject
to its [terms of service](https://mcp.tex64.com/mathpoint/terms).
