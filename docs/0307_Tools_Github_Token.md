---
Title | Tools Github Token
-- | --
Created @ | `2024-06-20T06:12:07Z`
Updated @| `2024-06-20T06:12:07Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/307)

---
# Develop with Github `personal access token`

## Github Setup

- `Settings` -> `Developer Settings` -> `Personal access tokens` -> `Tokens(classic)` -> `Generate new token`

![image](https://github.com/junxnone/xwiki/assets/2216970/9714168a-c374-4d2c-8cd2-b180701fd4d7)

> [!note]
> 保存好 token 备用


## Host 端设置


```

git_repo_token=ghp_ZoDxxxx
git_username="your_user_name"
git config --global user.name  $git_username
touch ~/.git-credentials
echo "https://$git_username:$git_repo_token@github.com" > ~/.git-credentials
git config --global credential.helper store
git config --global user.name  $git_username
touch ~/.git-credentials
echo "https://$git_username:$git_repo_token@github.com" > ~/.git-credentials
git config --global credential.helper store
cat << EOF > ~/.netrc
machine github.com
  login not-used
  password $git_repo_token
machine api.github.com
  login not-used
  password $git_repo_token
EOF

```