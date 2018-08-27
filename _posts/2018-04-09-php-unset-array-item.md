---
layout: post
category: programming_language
title: "PHP unset数组对象测试"
tags: PHP unset array
---

# PHP unset数组对象测试
* 测试从数组中unset掉一个元素后的数组结构
* unset为直接从数组中删除对应元素
* 被删除元素对应的index值会空缺
* index值不连续的数组仍可以使用foreach方式遍历

## 测试代码
```
$a = array(
    'first', 'second', 'third'
);

//var_dump($a);
foreach($a as $k => $v) {
    echo "{$k}:{$v}\n";
}
echo "\n";

$b = $a;
unset($b[0]);
//var_dump($b);
foreach($b as $k => $v) {
    echo "{$k}:{$v}\n";
}
echo "\n";

$b = $a;
unset($b[1]);
//var_dump($b);
foreach($b as $k => $v) {
    echo "{$k}:{$v}\n";
}
echo "\n";

$b = $a;
unset($b[2]);
//var_dump($b);
foreach($b as $k => $v) {
    echo "{$k}:{$v}\n";
}
echo "\n";
```
