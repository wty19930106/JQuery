# JQuery #
## JavaScript的类库 ##

将一些复杂但是复用率高的逻辑，封装起来，直接调用,大大减少了代码量
对于低版本浏览器的兼容是处理过的，无须担心因为兼容问题程序挂了的
支持运动。特别是在操作DOM，ajax中有着优先、杰出的表现.
## JQ常用选择器 ##

	$('#div') id选择器
	$('.li') class选择器
	$('input[type="button"]')  属性选择器
	
	$('li[class*="li"]') 属性通配选择器
	
	$('li[class^="li"]') 属性开头选择器
	
	$('li[class$="li"]') 属性结尾选择器
	
	$('li[class!="li"]') 属性排除选择器
	
	$('li:odd') 奇数选择器 （从0开始计数）
	
	$('li:even') 偶数选择器 （从0开始计数）
	
	$('li:gt(3)') 大于选择器
	$('li:lt(3)') 小于选择器
	$('li:eq(3)') 下标选择器
## JQ常用属性操作 ##

	val()  =  vlaue
	
	html()  = innerHTML
	
	text() = innerText
	
	addClass('xxx') => className = 'xxx' 
	
	removeClass('xxx') => 删除指定的class名
	
	console.log(attr('index'))  -> getAttribute('index')
	
	attr('index','1')  -> setAttribute('index','1');
	
	注意：
	操作表单元素属性：checked，disabled ，统一使用prop

	$().each(function(i,e){//跟forEach参数对调
			
		})
		
	index(); //当前元素相对于兄弟元素的索引。
	尽量在写index()的时候，把范围传入到index()方法中。
	比如：
		index(':button') ; 从button中当前触发的元素索引为几
## 常用DOM ##
	document  id,className,tagName,appendChild
			
	DOM描述（Document Object Model）
		通过document提供的api赋予我们操作页面的能力
	
	
	1.DOM树的关系
	2.增删改查
	
	上一个  prev();
	下一个  next();
	子级 children();
	父级 parent();
	兄弟级 siblings();
	第一个 first()
	最后一个 last();

	closest：
	逐级向上级元素匹配，并返回最先匹配的元素,也包括自身。
	closest('范围')
### 模块暂存 ###
	find(必传搜索范围);找到某个元素下的所有子元素 （可以查找某个范围下的所有）
		
	children(支持搜索范围);//只能找一层
	*/
	//不推荐直接通过关系去选择元素，性能差。css选择器一样，先找i再找ul
	//	$('#ul i').text('1234');

	//建议下面的获取方式
	const ul = $('#ul');
	ul.find('i').text('1234');
	
	console.log(ul.children('.dd'));//查找一层
### 增删改查 ###
	创建：
		$('<li>') 没内容
		$('<li></li>') 有内容
	
	删除：
		remove()
		
	插入：
		append();
		appendTo()
		prepend():放到某个元素的第一位

	<p>I would like to say: </p>
	
	$("p").prepend("<b>Hello</b>");
	
	结果:
	[ <p><b>Hello</b>I would like to say: </p> ]
	after 就是插入到第二个的后面
		
	insertAfter 就是插入到第二个的后面
	
	insertBefore 就是把第5个插入到第三个的前面
### 深度克隆 ###
	.clone()方法深度 复制所有匹配的元素集合，包括所有匹配元素、匹配元素的下级元素、文字节点。 

	注意: 使用.clone()可能产生id属性重复的元素的副作用，id应该是唯一的。在可能的情况下，  
	建议，应避免克隆有此属性或标识符的元素，使用类（class）属性代替。 
## 常用BOM ##
	height()/width() 就是设置的宽高，不支持padding和border
		
	
	innerWidth()/innerHeight() 支持padding 不支持border
	设置：设置之后总的宽高为固定的某个值（不带border）。
	
	
	outerHeight/outerWidth 支持padding和border(获取的时候还支持margin)
	设置：设置之后总的宽高为固定的某个值。
	
	原生转jQ对象   $(原生对象)  -> JQ对象 
		
	JQ对象转原生  $('textarea').get(0) -> 原生对象
				
				 $('textarea')[下标] -> 原生对象
	绝对位置(当前元素到页面顶部的位置):
			offset().left/offset().top
			
		
	当前元素到定位父级的距离：
		position().top/position().left
		
	滚动距离：
		scrollTop/scrollLeft
## 运动 ##
	在hide或者show中设置时间之后，会有运动效果,改变宽、高 、透明度
		
		slow（慢），normal（中等），fast（快）

	jQ中的运动是走队列的。 
		
	只要使用jQ中的运动，那么就要加stop()
## 事件 ##
	jQ中所有的事件方法全是addEventListener事件绑定的
		
	并且所有的事件方法都是由on()来扩展出来的。

	在使用JQ中，碰到事件套事件，那么就会出现，多次触发父级事件的时候
	再触发一次子级事件，这个时候子级事件触发的频率跟父级触发是一样的。
		
	解决：
		使用off在子级事件函数前解绑。

	阻止冒泡与阻止默认行为都是return false;

	

### on的绑定数据 ###
	$.each()专门给非JQ对象使用的。（工具方法） $.

	const arr = [
		'第一条内容',
		'第二条内容',
		'第三条内容'
	];
	
	
	$.each(arr,function(i,e){
		var b = $(`<button>按钮${i+1}</button>`).on('click mouseover',{a:arr[i],id:i},function(ev){
			console.log(ev.data);
		});
		
		$('body').append(b);
	});

### 事件监听 ###
	1.事件必须绑定在父级身上
	2.当触发某个事件的时候，通过事件冒泡，使得父级可以从ev.target中监听到当前触发的元素
	  是否为想要的子级
	3.如果是就执行事件处理函数。

	$('ul').on('click','li',function(){
		$(this).css('background','red');
	});