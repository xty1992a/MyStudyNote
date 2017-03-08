##2.jquery选择器$(selecter)
###基本选择器
- '#id'				 根据ID选择对应DOM,将其转为 jquery对象
- '.className' 		根据类名选择一组DOM,将其转为jquery对象
- '&lt;tagName&gt;'  		 根据标签名选择一组DOM,将其转为jquery对象
- '*'   				选择页面内所有元素,将其转为jquery对象
		
###关系选择器
- 'selector1,selector2,selector3' 			并集选择器
- 'selector1selector2selector3' 			  交集选择器
- 'selector1 > selector2'  				   子元素选择器
- 'selector1 selector2'		 			  后代选择器
- 'selector1 + selector2'		 		    下一个兄弟
- 'selector1 ~ selector2'		 		    后面所有兄弟
	
####过滤选择器(根据特点选择出指定元素)
- ':first'/':last'/':not'/':lt'/':gt'		 根据位置选择
- ':hidden'/':visible'						根据可见性选择
- ':contains(text)'							根据内容选择
- '[attrName]'/'[attr=value]'				 根据属性选择	
- ':animated'									正在动画中的
- 'lt'/'gt'/'eq'								根据索引指定
	- '	


###表单选择器
- :input'/':checkbox'/':text'                 表单项:'
- ':checked'								  已选中的
- ':selected'							     已选中的
- ':disabled'							     不可用的
			
###筛选			

			
			
			
			
			
			
			
			
			
			