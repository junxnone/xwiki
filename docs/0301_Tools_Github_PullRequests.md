---
Title | Tools Github PullRequests
-- | --
Created @ | `2024-04-06T04:24:37Z`
Updated @| `2024-04-06T04:25:45Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/301)

---
``` mermaid
flowchart TD
    A[1 Fork the repo] -->B[2 Clone the repo to Local]
    B --> B1(New Branch)
    B1 --> C(3 Develop)
    C --> E[5 Commit]
    E --> E1[push to the new barnch of fork]
    E1 --> F[6 Pull Request from web]
    F --> F1[CI Test & Review]
    F1 -->|looks good| F2[Merge]
    F1 -->|failed| N[Fix Bug]
    N --> E
```


## Reference

- [Pull Request Workflow with Git](https://medium.com/@urna.hybesis/pull-request-workflow-with-git-6-steps-guide-3858e30b5fa4)
