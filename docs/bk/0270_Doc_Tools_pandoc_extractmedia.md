-----

| Title     | Doc Tools pandoc extractmedia                        |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-06-24T06:08:02Z`                               |
| Updated @ | `2023-06-24T06:08:02Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/270) |

-----

# Pandoc: `提取媒体文件`

  - `input.md` --\> `output.md`
  - `images` -\> `media/`

<!-- end list -->

    pandoc --wrap=preserve -f markdown input.md --extract-media=media -t markdown -o output.md
