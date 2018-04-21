---
title: "Play With Tanakh"
date: 2018-04-21T19:03:26+08:00
---

[mattn](https://github.com/mattn)大神发了一个莫名很萌的[脚本](https://gist.github.com/mattn/bb81b6b78870ace119ca08c9819d4f4d/revisions)

```
#!/bin/bash

function stop() {
  tput cnorm
  echo
  exit
}

trap stop SIGINT

tput civis
while true; do
  while read line; do
    echo -e -n "\r$line\x1b[K"
    sleep 0.2
  done <<'EOF'
　(´･_･`)´･_･`)
　 (´･_･`)_･`)
　  (´･_･`)`)
　  ((´･_･`)
　 (´･(´･_･`)
　(´･_(´･_･`)
　(´･_･`)´･_･`)
　 (´･_･`)_･`)
　  (´･_･`)`)
　   (´･_･`))
　  ((´･_･`)
　 (´･(´･_･`)
　 (´･_(´･_･`)
EOF
done
```

这里面有些bash的东西，平时不怎么用到，查过后才知道是什么意思，这里稍微做下记录。

## `tput`

`tput cnorm`可以用来显示cursor。

`tput civis`可以用来隐藏cursor。

## `trap stop SIGINT`

`trap`用来给`SIGINT`绑定一个handler，这里就是`stop`这个函数。

## `echo -e -n "\r$line\x1b[K"`

`-e`用来开启解释`\`后的转义。

`\r` (Carriage Return) - moves the cursor to the beginning of the line without advancing to the next line

`\n` (Line Feed) - moves the cursor down to the next line without returning to the beginning of the line - In a *nix environment \n moves to the beginning of the line.

`\r\n` (End Of Line) - a combination of \r and \n

所以，`\r`和`\n`真的不一样。。。如果把脚本里的`\r`换成`\n`，会生成鬼畜的双螺旋表情。

```
printf("\x1b[%uD", n);  /* move cursor n steps to the left */
printf("\x1b[%uC", n);  /* move cursor n steps to the right */
printf("\x1b[K");       /* clear line from cursor to the right */
printf("\x1b[1K");      /* clear line from cursor to the left */
printf("\x1b[2K");      /* clear entire line */
```
Ref: https://stackoverflow.com/questions/7896508/intermediate-command-line-interfaces

所以，`\x1b[K`在这里主要用来清理掉上次循环遗留的表情。
