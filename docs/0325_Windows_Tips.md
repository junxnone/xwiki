---
Title | Windows Tips
-- | --
Created @ | `2026-05-19T05:50:12Z`
Updated @| `2026-05-19T05:52:01Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/325)

---
# Windows Tips

## 查询远程有没有人 RDP 连接上桌面

```
query user
```
> 必须开通 ssh 连接的情况下，连上去查询

- 未连接
```
 USERNAME              SESSIONNAME        ID  STATE   IDLE TIME  LOGON TIME
xxxxx                                     1  Disc         2:13  5/19/2026 2:10 AM
```

- 连接中
```
USERNAME              SESSIONNAME        ID  STATE   IDLE TIME  LOGON TIME
 xxxxx                 rdp-tcp#0           1  Active          .  5/19/2026 17:10
```
