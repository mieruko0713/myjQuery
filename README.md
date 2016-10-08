# jQuery效果实现集合

## 
前言： jQuery的书，从《jQuery基础教程》到《锋利的jQuery》再到《精通jQuery》，讲道理，这段刷书的经历让我深深感受到了光说不练假把式这句话的真义。。。。😂，于是开始对jQuery实际页面效果进行狂轰滥炸式练习，素材来自各个已上线网站，仅作练习用哈。    

## 坑
### 09.28踩坑纪录   
    - 商品多条件筛选中 商品标签的关闭按钮事件绑定失败 无语法错误 但是事件处理程序不执行    
    - 全选反选不选练习中，如果我一开始就点一次不选，那么再点全选就会失败
### 10.08填坑
- 商品多条件筛选中这个问题，主要在于jQuery的on方法是无法绑定动态生成的元素的。解决方案是把元素的父元素找出来，然后把事件委托给父元素，这样就没有问题了。

### 09.28 重要的知识    
#### queue方法会终结一个链式调用
之前看书的时候就知道动画与动画之间是排队的，而动画与其它类型方法（比如css()）是不排序的。在仿仙剑官网人物角色切换这个demo中，有这样一段代码:    
```js
$(".role-body img").fadeOut().queue(function(next){
    $(this).attr("src",imgs[i]);
    next();
}).fadeIn();
```
这里我为了让attr也排序，调用了queue方法，把attr放进queue方法中，它就可以进行排队，但是如果不往里面传入next参数并且对next参数进行调用，那么整个链式调用会到此为止，然而我们很明显不希望这样。因此，如果queue方法后面仍然有方法待执行，那么就需要在queue中调用next函数。
    
### 09.29踩坑纪录 
#### animate回调函数提前执行
职业介绍切换特效里面，切换动作特别快的时候，内容撤出动画就没有了，直接消失然后移入新动画。测试一中午，百思不得其解。    
 
### 09.29 重要的知识
#### parent方法和parents方法
parent方法的搜索范围是当前节点的上层节点，parents方法的搜索范围是当前节点的所有祖先节点   
#### stop的两个参数
stop(参数1，参数2)，参数1:是否停止所有运动，参数2:是否在当前运动的终点停止运动

