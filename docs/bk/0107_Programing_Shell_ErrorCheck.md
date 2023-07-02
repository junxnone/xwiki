-----

| Title         | Programing Shell ErrorCheck                          |
| ------------- | ---------------------------------------------------- |
| Created @     | `2019-05-28T05:56:22Z`                               |
| Last Modify @ | `2022-12-22T06:44:47Z`                               |
| Labels        | \`\`                                                 |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/107) |

-----

# 错误检查

## Reference

  - [shell
    管道和tee使用时获取前面命令返回值](https://www.cnblogs.com/double12gzh/p/10287226.html)

## Brief

  - shell中使用符号 `$?` 来显示上一条命令执行的返回值
      - 返回值为 `0` 则代表执行成功
      - 其他表示失败
  - **PIPESTATUS** 是一个数组,记录了上一条管道命令中所有的返回值
      - PIPESTATUS\[0\]: 第1个命令
      - PIPESTATUS\[1\]: 第2个命令
      - PIPESTATUS\[2\]: 第3个命令

## UseCase

  - `$?`

<!-- end list -->

    if [ $? -ne 0 ]; then
        echo "failed"
        exit 0
    else
        echo "succeed"
    fi

  - `PIPESTATUS`

<!-- end list -->

    $ cat 1238|ls
    cat: 1238: No such file or directory
    
    $ echo ${PIPESTATUS[0]}${PIPESTATUS[1]}
    10

## tee 未收集 error log

  - 添加 `2>1&`

<!-- end list -->

    your_cmd 2>1&|tee your_log.txt
