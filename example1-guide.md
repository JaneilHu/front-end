使用 jQuery 实现网页定位导航

技术点：
1.锚点（anchor）：命名锚记，页面内的超链接，可在文档中设置标记，这些标记存放在文档的顶部。
2.滚动条定位的事件和方法：
	scroll([data],fn):当用户滚动指定的元素时，会发生scroll事件。
	例如$(window).scroll(function(){});
	scrollTop([val]):获取/设置匹配元素相对滚动条顶部的偏移。
	offset():获取匹配元素的相对偏移。