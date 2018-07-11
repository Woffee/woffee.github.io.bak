---
layout: post
title:  "发现了一个PHP的坑点"
date:   2018-07-11 11:33:00 +0800
categories: dev
---

我向来很喜欢PHP的关联数组，因为它与json之间的转换是如此的“完美”。

但是，最近由于一个相关的bug，我改变了这一点。

为了说明这个bug，我写了一段测试代码：


	$arr1 = ['a','b','c'];
	$arr2 = ['a','b','c','a','d'];

	echo json_encode(array_unique($arr1))."\n";
	echo json_encode(array_unique($arr2))."\n";

	//该段代码输出的结果为：

	["a","b","c"]
	{"0":"a","1":"b","2":"c","4":"d"}

### 发现坑点了吗？

**按照常理，相同的代码，处理相同的数据，应该会得到类似的结果。**

然而，这段代码输出的结果中，第一行的json字符串表示的是一个数组；第二行却表示的是一个对象！另一个程序在解析的时候就会出错！

### 为什么呢？

$arr1 数组和 $arr2 数组，唯一的不同就是：$arr2中，'a'元素出现了两次。我们打印一下$arr1 和 $arr2 经过 array_unique 处理后的结果：

	$arr1 = ['a','b','c'];
	$arr2 = ['a','b','c','a','d'];

	var_dump(array_unique($arr1));
	var_dump(array_unique($arr2));

	//该段代码输出的结果为：

	array(3) {
	  [0]=>
	  string(1) "a"
	  [1]=>
	  string(1) "b"
	  [2]=>
	  string(1) "c"
	}
	array(4) {
	  [0]=>
	  string(1) "a"
	  [1]=>
	  string(1) "b"
	  [2]=>
	  string(1) "c"
	  [4]=>
	  string(1) "d"
	}

原来，$arr2 中的 3=>'a' 被 array_unique 去除了，导致数组的数字索引不连贯，从而 json_encode 将其当作对象处理来编码。

### 我的解决方法

在使用 array_unique 后，再使用 array_values 处理一下，使索引连续。

### 总结

一个字：坑。我们当然都希望程序能够处理各种不同数据，但是这种“自作聪明”的处理方式需要格外小心。