-----

| Title     | Programing Python Tools yapf                        |
| --------- | --------------------------------------------------- |
| Created @ | `2019-11-14T05:59:05Z`                              |
| Updated @ | `2024-04-23T02:14:01Z`                              |
| Labels    | \`\`                                                |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/93) |

-----

# yapf 代码格式化工具

  - **Google 开发的一款python code 格式化工具**

## UseCase

  - 查看会更改哪些内容

<!-- end list -->

    yapf -d your_code.py

  - 直接替换源文件

<!-- end list -->

    yapf -i your_code.py

  - style: 可选 `pep8` 或 `google` , 默认是 `pep8`

<!-- end list -->

    yapf -i --style google your_code.py

## Reference

  - [Github - Google](https://github.com/google/yapf)
