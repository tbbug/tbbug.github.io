---
layout: post
title: think-angular 模板引擎
categories: [小工具, solidity]
tags: [thinkphp, angular,webstrom, solidity]
status: publish
type: post
published: true
author: blackfox
permalink: /20180806/block-chain-technical-guide.html
keyword: idea,webstrom,phpstorm solidity 
desc: for循环
---

> for循环

```
<div class="page">
    <a php-show="$p > 1" href="/article/lists?p={$p-1}">上一页</a>
    <a php-for="$i = $page_start; $i <= $page_end; $i++" href="/article/lists?p={$i}">第{$i}页</a>
    <a php-show="$p < $page_count" href="/article/lists?p={$p+1}">下一页</a>
</div>
```

解析后:

```
<div class="page">
    <?php if ($p > 1) { ?>
        <a  href="/article/lists?p=<?php echo $p-1; ?>">上一页</a>
    <?php }  for ($i = $page_start; $i <= $page_end; $i++) { ?>
        <a  href="/article/lists?p=<?php echo $i; ?>">第<?php echo $i; ?>页</a>
    <?php }  if ($p < $page_count) { ?>
        <a  href="/article/lists?p=<?php echo $p+1; ?>">下一页</a>
    <?php } ?>
</div>
```