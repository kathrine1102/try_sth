#this.index 与 i
>第一句：给oLis中的所有元素设置一个索引值，便于查找
第二句：设置oDivs中的this.index元素中的className为空
this.index就是你所点击li元素的索引所对应的div元素

因为页面一旦加载完成就触发onload事件,而onclick事件触发之前,for(var i= 0,len = oLis.length;i<len;i++)这个循环已经运行完成了!oLis[i].onclick = function()这段代码只是挂在那里(挂这个词不怎么准确,意思放在那里,等待onclick事件触发),这时候的i=3.在oLis[i].onclick = function()之前document.writeln(i)你会发现输出012,说明循环已经完成.

>oLis[i].index = i 的作用只是在循环的过程中绑定下标i(0 1 2)到oLis数组相应元素oLis[0] oLis[1] oLis[2]的index变量上(例如oLis[0].index = 0;oLis[1].index =1;oLis[2].index=2)

当onclick事件触发的时候,this.className中的this就是当前鼠标所在的元素(例如家居), 同时oDivs[this.index]会获取到家居所对应的oLis数组中的index值(这里是1,因为我们已经在完成的循环中将oLis[1]=1 了),而如果换成oLis[i]则因为i===3(恒等于3),所以oLis[i]===oLis[3],当然会出错了!建议好好看一下JS的闭包原理和事件机制!


<html lang="en">
<head>
	<meta charset="UTF-8">
	<style>
		input
		{
			background: #fff;
			cursor: pointer;
			outline: none;
		}
		.active
		{
			background: yellow;
		}
		div
		{
			display: none;
			width: 200px; height: 200px;
			background: pink;
		}
	</style>
<body>
	<form action="">
		<input class="active" type="button" value="1">
		<input type="button" value="2">
		<input type="button" value="3">
	</form>
	<div style="display: block;">111</div>
	<div>222</div>
	<div>333</div>
	
<script>
	window.onload=function()
	{
		var aBtn=document.getElementsByTagName('input');
		var aDiv=document.getElementsByTagName('div');
		var i;
		for(i=0;i<aBtn.length;i++)
		{
			aBtn[i].index=i;
			aBtn[i].onclick=function()
			{
				for(i=0;i<aBtn.length;i++)
				{
					aBtn[i].className='';
					aDiv[i].style.display='none';
				}
				this.className='active';
				aDiv[this.index].style.display='block';
			}
		}
	}
</script>

</body>
</html>