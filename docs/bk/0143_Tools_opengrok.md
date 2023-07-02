-----

| Title     | Tools opengrok                                       |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-04-20T16:08:54Z`                               |
| Updated @ | `2023-03-28T14:27:40Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/143) |

-----

# opengrok 代码浏览工具

  - 浏览代码用的Web工具
  - 可以实现较快的跳转搜索
  - 可以使用 docker 部署

## Setup With Docker

  - **Pull opengrok docker image**

<!-- end list -->

    docker pull opengrok/docker

  - **Run container**

<!-- end list -->

    docker run -d -v <path/to/your/src>:/opengrok/src -p 8080:8080 opengrok/docker:latest

> e.g. `docker run -d -v ~/workm/opengrok_src:/opengrok/src -p 8080:8080
> opengrok/docker:latest`

  - **Manually trigger an reindex**

<!-- end list -->

    docker exec <container> /scripts/index.sh

## Reference

  - <https://oracle.github.io/opengrok/>
  - [opengrok Docker](https://hub.docker.com/r/opengrok/docker/)
