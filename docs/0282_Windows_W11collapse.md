---
Title | Windows W11collapse
-- | --
Created @ | `2023-07-18T08:24:51Z`
Updated @| `2023-07-18T08:24:51Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/282)

---
# Win11 关闭右键菜单折叠

- <kbd>Win</kbd> + <kbd>R</kbd>
- **选择项:** `HKEY_CURRENT_USER\Software\Classes\CLSID`
- **右键单击CLSID新建项：**`{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}`
- **在新创建好的项下创建子项:** `InprocServer32`, 并修改默认值为 `1`
- **重启电脑**
