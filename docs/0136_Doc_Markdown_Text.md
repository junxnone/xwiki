---
Title | Doc Markdown Text
-- | --
Created @ | `2021-09-22T10:02:45Z`
Last Modify @| `2022-12-27T01:06:16Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/136)

---
# Text Format

## 对齐

- **居中对齐**

```
<p align="center ">Here is left</p>
```
<p align="center ">Here is center</p>  

- **左对齐**  
```  
<p align="left">Here is left</p>
```
<p align="left">Here is left</p>

- **右对齐**
```
<p align="right">Here is right</p>
```
<p align="right">Here is right</p>

- superscript & subscript

```
Text Line<sup>superscript</sup>
Text Line<sub>subscript</sub>
```
Text Line<sup>superscript</sup>  
Text Line<sub>subscript</sub>

##  **转义字符**

```
\* \` \|
```
\* \` \|

## **引用**

```
> 1级引用
>> 2级引用
>>> 3级引用
```
> 1级引用
>> 2级引用
>>> 3级引用

### **Code 引用**

Github issues markdown 引用 code
只能是本repo的code
例如
https://github.com/junxnone/wiki/blob/cbdf0ee17452e221607ae78b5e1ecb5af546cf94/index.04eb6053.js#L5-L7


## 隐藏
```
<!-- 你看不到我看不到我 -->
```
- a
- <!-- 你看不到我看不到我 -->
- c

### 折叠隐藏

````
<details>
<summary>折叠世界</summary>
Hello， 这里是折叠世界

```
Code
Code
```

</details>
````

<details>
<summary>折叠世界</summary>
Hello， 这里是折叠世界

```
Code
Code
```

</details>

## **Keyboard 格式**

```
<kbd>ctrl</kbd> + <kbd>c</kbd>
```
<kbd>ctrl</kbd> + <kbd>c</kbd>



