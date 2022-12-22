---
Title | Features IncludeContent
-- | --
Created @ | `2021-11-07T06:47:14Z`
Last Modify @| `2022-12-21T07:52:07Z`
Labels | `Features`
Edit @| [here](https://github.com/junxnone/twiki/issues/13)

---
# Include Content

## wikilink

[[hist]]

## Include doc

```
[update](hist.md ':include')
```

--- Included docs start ---

[update](hist.md ':include')

--- Included docs end ---

## Include code


```
[update](hist.md ':include :type=code')
```


[update](hist.md ':include :type=code')

## Include gist

```
[gist: hello_openmp](https://gist.githubusercontent.com/junxnone/9af88e64446fb0746ebfb1e0e8879f33/raw/2d04dcd1fd3ac51988d3e756bb1be477efe02216/openmp_helloworld.cpp ':include :type=code')
```
- 如果要使用 `gist` 的最新内容需要 把 `commit id` 移除 

```
https://gist.githubusercontent.com/junxnone/9af88e64446fb0746ebfb1e0e8879f33/raw/openmp_helloworld.cpp
```

[gist: hello_openmp](https://gist.githubusercontent.com/junxnone/9af88e64446fb0746ebfb1e0e8879f33/raw/openmp_helloworld.cpp ':include :type=code')

## Include web

```
[junxnone website](https://junxnone.github.io ':include :type=iframe width=100% height=1200px')
```

[junxnone website](https://junxnone.github.io ':include :type=iframe width=100% height=1200px')


## Include pdf file

- **plugin** [docsify-pdf-embed](https://github.com/lazypanda10117/docsify-pdf-embed)

[gist: include pdf file](https://gist.githubusercontent.com/junxnone/2efa4f014527293cd2950b8aff96f488/raw/docsify_include_pdf_file ':include :type=code')


```pdf
flann_docs.pdf
```

## include embed iframe

[junxnone website](https://codepen.io/syt123450/embed/YRwZGg?default-tab=html%2Cresult ':include :type=iframe width=100% height=1200px')

