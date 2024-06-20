-----

| Title     | Tools Github SSHKey                                  |
| --------- | ---------------------------------------------------- |
| Created @ | `2018-12-12T09:21:02Z`                               |
| Updated @ | `2024-06-20T06:07:02Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/123) |

-----

# Github Access with ssh key

  - Generate the github token for ssh access

## Steps

  - **1 Generate the key**

<!-- end list -->

    ssh-keygen
    cat .ssh/id_rsa.pub

  - **2 copy the publickey to the github**

![image](media/f34e3c9fdd1a10088ffbe77d70e7ada6c4940f40.png)
![image](media/62a89d5718390492bbd31ae8f5e6075736ee1b3a.png)

`  ssh-rsa
xxxxxxxxxxxxxxxxxxxxxABAQC4OI93xICB3nyCM57MGXu1t/ZVBrvqsaZCrEokOOHzWHbd3UdEmALRkrm9U0srP8VBVdYcv6RSE0tYSntuN+tT6BJmzOMRMPbDnXJyHniDsFtzQcbrZd6RPKXXsk4Bhnjxtx2dNBdJkOXoWIGH2sK0Nbt5Z2jqF8DPF8AWIkuK66YOtazkPCLzddTl8EWMinLH/Zr55Pw940MTPIswDu3sYzQJBFZ2z+85t3jwFH/O2ZmrZmqtEKHu0IDeakUDZxxxxxxxxxxxxxxxxxxxxxxxx
name@hostname `

## Reference

  - [Generating a new SSH key and adding it to the
    ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
