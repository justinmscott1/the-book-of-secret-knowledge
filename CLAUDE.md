# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this repo is

A fork of [trimstray/the-book-of-secret-knowledge](https://github.com/trimstray/the-book-of-secret-knowledge): a curated list of tools, manuals, cheatsheets, blogs, and shell one-liners for sysadmins, DevOps, pentesters, and security researchers.

There is no code, build, or test suite. Nearly all content lives in one file, `README.md` (~4,400 lines).

```
README.md                  # the whole book
LICENSE.md                 # MIT
.github/CONTRIBUTING.md    # contribution rules, broken-link check script
.github/CODE_OF_CONDUCT.md
.github/FUNDING.yml
static/img/                # preview image used at the top of README.md
```

## README.md structure

- Intro sections use `## :emoji: &nbsp;Title`.
- Each chapter is a level-4 heading with a back-link to the main TOC:
  `#### CLI Tools &nbsp;[<sup>[TOC]</sup>](#anger-table-of-contents)`
- The main TOC (`## :anger: &nbsp;Table of Contents`) links chapters by their GitHub slug, e.g. `#cli-tools-toc`. When adding or renaming a chapter, update the TOC to match.
- Chapters, in order: CLI Tools, GUI Tools, Web Tools, Systems/Services, Networks, Containers/Orchestration, Manuals/Howtos/Tutorials, Inspiring Lists, Blogs/Podcasts/Videos, Hacking/Penetration Testing, Your daily knowledge and news, Other Cheat Sheets, Shell One-liners, Shell Tricks, Shell functions.

### Link-list chapters (CLI Tools through Other Cheat Sheets)

Subsections are `##### :black_small_square: Name`, followed by a `<p>` block of entries in raw HTML, one per line:

```html
<p>
&nbsp;&nbsp; <a href="https://www.zsh.org/"><b>Zsh</b></a> - is a shell designed for interactive use, although it is also a powerful scripting language.<br>
</p>
```

- Keep the `&nbsp;&nbsp;` indent, bold name inside the link, ` - ` separator, lowercase description, and trailing `<br>`.
- A trailing `<b>*</b>` (before `<br>`) marks a URL as temporarily unavailable. Do not delete such entries unless the link is confirmed permanently dead.

### Shell One-liners

- Starts with its own `##### Table of Contents` listing `* [tool](#tool-tool)` anchors; keep it in sync with the tool sections.
- Each tool is `##### Tool: [name](url)`, each recipe a `###### Short description` followed by a fenced `bash` block.

## Contribution rules (from `.github/CONTRIBUTING.md` and the README)

- Only good-quality material; the list is not meant to contain everything.
- Match the existing formatting exactly; don't reformat unrelated lines (keeps diffs reviewable in a 4,400-line file).
- Commits upstream carry a `signed-off-by` line; the upstream author's style is `short message - signed-off-by: Name <email>`.
- PRs: base on latest `master`, explain the problem and solution, one-line description.

## Checking links

The broken-link check from CONTRIBUTING.md:

```bash
for i in $(sed -n 's/.*href="\([^"]*\).*/\1/p' README.md | grep -v "^#") ; do
  _rcode=$(curl -s -o /dev/null -w "%{http_code}" "$i")
  if [[ "$_rcode" != "2"* ]] ; then echo " -> $i - $_rcode" ; fi
done
```

Redirects (3xx) and rate-limited sites show up here too, so confirm a link is really gone before removing it.
