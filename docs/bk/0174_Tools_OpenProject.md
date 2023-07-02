-----

| Title         | Tools OpenProject                                    |
| ------------- | ---------------------------------------------------- |
| Created @     | `2019-07-14T05:21:08Z`                               |
| Last Modify @ | `2022-12-22T08:06:36Z`                               |
| Labels        | \`\`                                                 |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/174) |

-----

# OpenProject 项目管理工具

## Reference

  - [Github](https://github.com/opf/openproject)
  - [Install with Docker](https://www.openproject.org/docker/)
  - [Docker image](https://hub.docker.com/r/openproject/community/)

## Brief

  - project management software

## Install with Docker

**Pull image**

    docker pull openproject/community

**Run Container**

    docker run -itd -p 8090:80 -e SECRET_KEY_BASE=secret openproject/community

> access the websit: xxx.xxx.xxx.xxx:8090

## UseCase

![image](media/544c45566da7e7381961c3702c6f1afef916389b.png)
