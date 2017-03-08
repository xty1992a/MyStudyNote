##CSS选择器
http://www.w3school.com.cn/cssref/css_selectors.asp
- `.class`:类选择器
- `#ID`:ID选择器
- `*`:通配选择器
- `element`:元素选择器,选择所有指定标签名的元素
- `ele1,ele2`:并集选择器
- `ele1ele2`:交集选择器
- `ele1 ele2`:后代选择器
- `ele1>ele2`:子元素选择器
- `ele1+ele2`:紧邻兄弟选择器,选择紧邻ele1的ele2元素
- `ele1~ele2`:紧随兄弟选择器,选择前面有ele1的ele元素
- `[attribute]`:属性选择器,选择所有有指定属性的元素
- `[attribute=value]`:属性值选择器,选择所有指定属性值为指定值的元素
- `[attribute~=value]`:属性值包含选择器,包含指定属性值为指定值的元素 
- `[attribute^=value]`开头`[attribute$=value]`:结尾`[attribute*=value]`包含`
- `[attribute|=value]`:属性值头选择器,指定属性值以指定值开头的元素
伪类选择器
- `:link``:visited``:hover``:active`:a标签的四种伪类选择器
- `:focus`:获取焦点伪类选择器
- `:first-letter``:first-line``:first-child``:before``:after``:lang`
