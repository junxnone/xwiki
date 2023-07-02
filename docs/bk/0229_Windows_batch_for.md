-----

| Title     | Windows batch for                                    |
| --------- | ---------------------------------------------------- |
| Created @ | `2021-08-24T02:38:24Z`                               |
| Updated @ | `2023-03-27T14:41:49Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/229) |

-----

## Reference

  - [bat for循环\_解放双手！ bat
    批处理自动化运行程序](https://blog.csdn.net/weixin_39738380/article/details/110105571)

## UseCase

  - 循环执行 10 次，每次重命名结果文件

<!-- end list -->

    @echo off
    for /l %%a in (1,1,10) do (
        app.exe
        ren results.txt "results_%%a.txt"
    
    )
