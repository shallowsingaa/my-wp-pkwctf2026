# My WriteUp - PKWCTF2026

>**参赛队伍：** `​SuperSpider`

>**选手ID：** `sha11owSlng_Mz` 或 `shallowSingMz`（中途改名来着）

>**赛道：** 校内、新生

>**注：** 解题时有大量 AI 成分，wp全文为纯手搓。Orz. Orz.

>**github：** 

## 0x00 -> 目录

- [My WriteUp - PKWCTF2026](#my-writeup---pkwctf2026)
  - [0x00 -\> 目录](#0x00---目录)
  - [0x01 -\> Web](#0x01---web)
    - [01. 签到题【入门】](#01-签到题入门)
    - [02. mio上传【入门】](#02-mio上传入门)
  - [0x02 -\> Re](#0x02---re)
  - [0x03 -\> Pwn](#0x03---pwn)
  - [0x04 -\> Crypto](#0x04---crypto)
  - [0x05 -\> Misc](#0x05---misc)

## 0x01 -> Web

### 01. 签到题【入门】

*题干：*

```text
答案隐藏于页面的本源之中。常规的浏览方式无法寻觅，或许换一种途径能找到答案。
```

*解：*

F12 —— 元素 —— 找到奇怪的注释

![img_0x01.01.001](images/img-20260927033159_msedge.jpg)

得到 `UEtXQ1RGe2U0MmM3MDBkLTBkMDMtNGQ5MC1iN2QzLTU0NTIzOTNlYmFjN30=`

在 [CyperChef](https://cyberchef.org/) 用 base64 解码（From Base64）即可。

*flag:*

`PKWCTF{e42c700d-0d03-4d90-b7d3-5452393ebac7}`

### 02. mio上传【入门】



## 0x02 -> Re



## 0x03 -> Pwn



## 0x04 -> Crypto



## 0x05 -> Misc