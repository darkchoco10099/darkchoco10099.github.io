---
layout: post
title: Vue +Element 实现导航栏收缩展开功能
tags: [前端开发, Vue, Element]
---

## Vue +Element 实现导航栏收缩展开功能

isCollapse: true，初始值为true
:collapse=“isCollapse”，是否水平折叠收起菜单（仅在导航栏 mode 为 vertical 时可用），值为true 或 false

```
<template>
	...
	<el-header >
	          <i class="el-icon-s-fold" @click="isC" ></i>
	 </el-header>
	...
	<el-menu  :collapse="isCollapse" class="el-menu-vertical">
		...
	</el-menu>
	...
</template>

12345678910111213
```

当导航栏展开后的样式，自定义宽度，长度自适应

```
<style>
	.el-menu-vertical:not(.el-menu--collapse) {
	    width: 200px;
	  }
</style>

1234567
```

点击事件isC()，循环取反

```
<script>
	data () {
		return {
      		isCollapse: true
      	}
      }，
      methods: {
		    isC(){
		      this.isCollapse = !this.isCollapse
		    }
	  }
</script>

1234567891011121314
```

效果图：

当isCollapse为true，导航栏收缩
![img](https://www.codeleading.com/imgrdrct/https://img-blog.csdnimg.cn/20191008231715998.PNG)

当isCollapse为false，导航栏展开
![img](https://www.codeleading.com/imgrdrct/https://img-blog.csdnimg.cn/20191008225657840.PNG)