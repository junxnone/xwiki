---
Title | Programing Python File
-- | --
Created @ | `2023-11-02T09:35:35Z`
Updated @| `2023-11-02T09:35:35Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/297)

---
# 文件操作

```
with open(file_path, 'w') as f:
    xxxx
```

## API
- read()
- readline()
- readlines()
- writelines()

## mode
- 读/写/追加

模式 | 描述
-- | --
r | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。
rb | 以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。
r+ | 打开一个文件用于读写。文件指针将会放在文件的开头。
rb+ | 以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。
w | 打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。
wb | 以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。
w+ | 打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。
wb+ | 以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。
a | 打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。
ab | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。
a+ | 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。
ab+ | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。




模式 | r | r+ | w | w+ | a | a+
-- | -- | -- | -- | -- | -- | --
读 | + | + |   | + |   | +
写 |   | + | + | + | + | +
创建 |   |   | + | + | + | +
覆盖 |   |   | + | + |   |  
指针在开始 | + | + | + | + |   |  
指针在结尾 |   |   |   |   | + | +


## Reference
- [open](https://docs.python.org/3/library/functions.html?highlight=open#open)
- [I/O Base Classes](https://docs.python.org/3/library/io.html?highlight=writeline#i-o-base-classes)