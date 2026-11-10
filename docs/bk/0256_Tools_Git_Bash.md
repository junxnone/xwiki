-----

| Title     | Tools Git Bash                                       |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-06-16T08:18:07Z`                               |
| Updated @ | `2026-11-10T06:06:58Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/256) |

-----

# git bash

  - Windows 下 git 工具提供了 git bash (`mingw64`)
  - 可以跑简单的处理脚本(Linux下的可以比较简单的移植过来)

Git Bash 是随 [Git for Windows](https://gitforwindows.org/) 安装的一个终端环境，由
**MSYS2**（`bash` + 一套精简的 GNU 工具）和 **mintty**（终端模拟器）组成。它让 Windows 上也能使用
`bash`、`grep`、`sed`、`awk`、`ssh` 等常见 Linux 命令。

## 组成与目录

| 项目            | 说明                                           |
| ------------- | -------------------------------------------- |
| 安装目录          | 默认 `C:\Program Files\Git`                    |
| `usr\bin`     | MSYS2 的工具，即下面清单里的 `bash`、`ls`、`grep`、`sed` 等 |
| `mingw64\bin` | 原生 Windows 程序，如 `git.exe`、`curl.exe`         |
| `etc\profile` | 启动脚本，可在 `~/.bashrc`、`~/.bash_profile` 中自定义   |
| `~`           | 用户主目录，对应 `%USERPROFILE%`                     |
| mintty        | 默认终端窗口，支持复制粘贴、颜色、字体，在标题栏右键 → Options 设置      |

> 清单里的 `.exe` 来自 MSYS2 的 `usr\bin`，Git Bash 里直接输入 `ls`、`grep` 即可，不用加后缀。

## 路径与盘符

  - Windows 的 `C:\Users\xxx` 在 Git Bash 里写成 `/c/Users/xxx`。
  - 反斜杠是转义符，路径用正斜杠 `/`；包含空格的路径要加引号。
  - 路径转换：`cygpath -u 'C:\Users\xxx'`（转成 Unix 风格）、`cygpath -w
    /c/Users/xxx`（转成 Windows 风格）。
  - 调用 Windows 原生程序时，MSYS2 会自动把形如 `/xxx` 的参数当作路径转换，这有时会造成误转换：

<!-- end list -->

``` bash
MSYS_NO_PATHCONV=1 docker run -v /c/data:/data image   # 关闭路径自动转换
MSYS2_ARG_CONV_EXCL='*' some.exe /flag                  # 或排除所有参数
```

## 常用技巧

``` bash
explorer .                       # 在资源管理器中打开当前目录
start file.pdf                   # 用默认程序打开文件
clip < file.txt                  # 把文件内容复制到 Windows 剪贴板
cat file.txt | clip
winpty python                    # 交互式程序（如 python、node）卡住/无输出时，用 winpty 包一层
dos2unix file / unix2dos file    # 换行符转换
file * | grep CRLF               # 找 CRLF 换行的文件
```

  - 交互式 Python / node 在 mintty 里不能正常输入输出，是因为 mintty 不是真正的 Windows 控制台，用
    `winpty` 包装即可（清单里的 `winpty.exe`）。
  - 想直接写成别名：`alias python='winpty python'`，放进 `~/.bashrc`。

## 脚本移植到 Windows 的注意

  - 脚本需保存成 **LF** 换行，CRLF 会让 bash 报 `$'\r': command not found`。可用
    `dos2unix` 转换，或设置 git `core.autocrlf`。见 [No newline at end of
    file](/0120_Tools_Git_NoNewline)。
  - 没有的命令：`apt`、`yum`、`systemctl`、`sudo`、`lsof`、`top`（有
    `ps`）等；管理员权限需要以管理员身份启动 Git Bash。
  - `ln -s` 默认复制而不是创建真正的符号链接，需要设置 `export MSYS=winsymlinks:nativestrict`
    并开启开发者模式/管理员权限。
  - 想要更完整的 Linux 环境，可选 WSL，或 MSYS2 本身（可 `pacman` 安装软件）。

## 补充软件

Git Bash 的工具集是精简版，缺少 `make`、`zip`、`jq`、`rsync` 等。简单的做法是把对应的 Windows 版
`.exe` 放进 `C:\Program Files\Git\usr\bin`（或加入 PATH），例如：

  - `jq`、`make`、`zip` 的 Windows 二进制，或通过 `winget`/`scoop` 安装。

## 已包含的工具清单

<details>
<summary>git bash tools list</summary>

    arch.exe*
    awk.exe*
    b2sum.exe*
    base32.exe*
    base64.exe*
    basename.exe*
    basenc.exe*
    bash.exe*
    bunzip2.exe*
    bzcat.exe*
    bzip2.exe*
    bzip2recover.exe*
    captoinfo.exe*
    cat.exe*
    chattr.exe*
    chcon.exe*
    chgrp.exe*
    chmod.exe*
    chown.exe*
    chroot.exe*
    cksum.exe*
    clear.exe*
    cmp.exe*
    column.exe*
    comm.exe*
    cp.exe*
    csplit.exe*
    cut.exe*
    cygcheck.exe*
    cygpath.exe*
    cygwin-console-helper.exe*
    d2u.exe*
    dash.exe*
    date.exe*
    dd.exe*
    df.exe*
    diff.exe*
    diff3.exe*
    dir.exe*
    dircolors.exe*
    dirmngr-client.exe*
    dirmngr.exe*
    dirname.exe*
    dos2unix.exe*
    du.exe*
    dumpsexp.exe*
    echo.exe*
    env.exe*
    envsubst.exe*
    ex.exe*
    expand.exe*
    expr.exe*
    factor.exe*
    false.exe*
    file.exe*
    find.exe*
    fmt.exe*
    fold.exe*
    funzip.exe*
    gawk-5.0.0.exe*
    gawk.exe*
    gencat.exe*
    getconf.exe*
    getfacl.exe*
    getopt.exe*
    gettext.exe*
    gkill.exe*
    gmondump.exe*
    gpg-agent.exe*
    gpg-connect-agent.exe*
    gpg-error.exe*
    gpg-wks-server.exe*
    gpg.exe*
    gpgconf.exe*
    gpgparsemail.exe*
    gpgscm.exe*
    gpgsm.exe*
    gpgsplit.exe*
    gpgtar.exe*
    gpgv.exe*
    grep.exe*
    groups.exe*
    gzexe*
    gzip.exe*
    head.exe*
    hmac256.exe*
    hostid.exe*
    hostname.exe*
    iconv.exe*
    id.exe*
    infocmp.exe*
    infotocap.exe*
    install.exe*
    join.exe*
    kbxutil.exe*
    kill.exe*
    ldd.exe*
    ldh.exe*
    less.exe*
    lessecho.exe*
    lesskey.exe*
    link.exe*
    ln.exe*
    locale.exe*
    locate.exe*
    logname.exe*
    ls.exe*
    lsattr.exe*
    mac2unix.exe*
    md5sum.exe*
    minidumper.exe*
    mintty.exe*
    mkdir.exe*
    mkfifo.exe*
    mkgroup.exe*
    mknod.exe*
    mkpasswd.exe*
    mktemp.exe*
    mount.exe*
    mpicalc.exe*
    msgattrib.exe*
    msgcat.exe*
    msgcmp.exe*
    msgcomm.exe*
    msgconv.exe*
    msgen.exe*
    msgexec.exe*
    msgfilter.exe*
    msgfmt.exe*
    msggrep.exe*
    msginit.exe*
    msgmerge.exe*
    msgunfmt.exe*
    msguniq.exe*
    mv.exe*
    nano.exe*
    nettle-hash.exe*
    nettle-lfib-stream.exe*
    nettle-pbkdf2.exe*
    ngettext.exe*
    nice.exe*
    nl.exe*
    nohup.exe*
    nproc.exe*
    numfmt.exe*
    od.exe*
    openssl.exe*
    p11-kit.exe*
    passwd.exe*
    paste.exe*
    patch.exe*
    pathchk.exe*
    perl.exe*
    perl5.36.0.exe*
    pinentry-w32.exe*
    pinentry.exe*
    pinky.exe*
    pkcs1-conv.exe*
    pldd.exe*
    pluginviewer.exe*
    pr.exe*
    printenv.exe*
    printf.exe*
    profiler.exe*
    ps.exe*
    psl.exe*
    ptx.exe*
    pwd.exe*
    readlink.exe*
    realpath.exe*
    rebase.exe*
    recode-sr-latin.exe*
    regtool.exe*
    reset.exe*
    rm.exe*
    rmdir.exe*
    rnano.exe*
    runcon.exe*
    rview.exe*
    rvim.exe*
    scp.exe*
    sdiff.exe*
    sed.exe*
    seq.exe*
    setfacl.exe*
    setmetamode.exe*
    sexp-conv.exe*
    sftp.exe*
    sh.exe*
    sha1sum.exe*
    sha224sum.exe*
    sha256sum.exe*
    sha384sum.exe*
    sha512sum.exe*
    shred.exe*
    shuf.exe*
    sleep.exe*
    sort.exe*
    split.exe*
    ssh-add.exe*
    ssh-agent.exe*
    ssh-keygen.exe*
    ssh-keyscan.exe*
    ssh-pageant.exe*
    ssh.exe*
    sshd.exe*
    ssp.exe*
    stat.exe*
    stdbuf.exe*
    strace.exe*
    stty.exe*
    sum.exe*
    sync.exe*
    tabs.exe*
    tac.exe*
    tail.exe*
    tar.exe*
    tee.exe*
    test.exe*
    tic.exe*
    tig.exe*
    timeout.exe*
    toe.exe*
    touch.exe*
    tput.exe*
    tr.exe*
    true.exe*
    truncate.exe*
    trust.exe*
    tset.exe*
    tsort.exe*
    tty.exe*
    tzset.exe*
    u2d.exe*
    umount.exe*
    uname.exe*
    unexpand.exe*
    uniq.exe*
    unix2dos.exe*
    unix2mac.exe*
    unlink.exe*
    unzip.exe*
    unzipsfx.exe*
    users.exe*
    vdir.exe*
    view.exe*
    vim.exe*
    vimdiff.exe*
    watchgnupg.exe*
    wc.exe*
    which.exe*
    who.exe*
    whoami.exe*
    winpty-agent.exe*
    winpty-debugserver.exe*
    winpty.exe*
    xargs.exe*
    xgettext.exe*
    xxd.exe*
    yat2m.exe*
    yes.exe*
    zipinfo.exe*

</details>

## Reference

  - [Git for Windows](https://gitforwindows.org/)
  - [MSYS2 路径转换](https://www.msys2.org/docs/filesystem-paths/)
  - [winpty](https://github.com/rprichard/winpty)
