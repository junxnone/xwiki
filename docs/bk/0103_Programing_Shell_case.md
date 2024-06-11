-----

| Title     | Programing Shell case                                |
| --------- | ---------------------------------------------------- |
| Created @ | `2020-05-04T08:09:42Z`                               |
| Updated @ | `2024-06-11T11:40:06Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/103) |

-----

# Shell case

    #!/bin/bash
    case $1 in
        1)
            echo '2'
            ;;
        2)
            echo '3'
            ;;
        *)
            echo 'haha'
    esac

## read input

    #!/bin/bash
    
    echo '
    #############################
        1.banana
        2.apple
        3.pear
        4.cherry
    #############################
    '
    read -p "please select a fruit：" fruit
    
    case $fruit in
        1)
            echo 'eat banana'
            ;;
        2)
            echo 'eat apple'
            ;;
        3)
            echo 'eat pear'
            ;;
        4)
            echo 'eat cherry'
            ;;
        *)
            echo 'eat nothing'
    esac

    source test_case.sh
    
    #############################
        1.banana
        2.apple
        3.pear
        4.cherry
    #############################
    
    please select a fruit：1
    eat banana

## Reference

  - [shell脚本中的case条件语句介绍和使用案例](https://www.cnblogs.com/guoke-boy/p/12605789.html)
