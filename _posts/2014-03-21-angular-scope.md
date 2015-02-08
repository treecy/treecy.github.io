---
layout: post
title: [转]深入理解 AngularJS 的 Scope
cover: cover.jpg
date:   2013-12-09 12:00:00
categories: posts
---

JavaScript 的原型继承就是奇葩。

之前在 V2EX 上看到讨论说，不会 OOP 的 JavaScript 的程序员就是野生程序员。看来我是属于野生的。

## 一、遇到的问题

问题发生在使用 AngularJS 嵌套 Controller 的时候。因为每个 Controller 都有它对应的 Scope（相当于作用域、控制范围），所以 Controller 的嵌套，也就意味着 Scope 的嵌套。这个时候如果两个 Scope 内都有同名的 Model 会发生什么呢？从子 Scope 怎样更新父 Scope 里的 Model 呢？

这个问题很典型，比方说当前页面是一个产品列表，那么就需要定义一个 ProductListController

	function ProductListController($scope, $http) {
	    $http.get('/api/products.json')
	        .success(function(data){
	            $scope.productList = data;
	        });
	    $scope.selectedProduct = {};
	}

## 二、解决的办法

解决的办法就是不使用基本数据类型，而在 Model 里永远多加一个点.
