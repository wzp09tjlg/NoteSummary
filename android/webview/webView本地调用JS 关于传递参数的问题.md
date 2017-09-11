当前使用webview越来越频繁，对于本地和webview的交互页变得频繁。
js是webview中经常嵌套使用的工具，怎么在本地调用js方法，webview已经提供api供我么调用。
在本地调用时 记得明确 需要怎么调用js，需要什么参数。如果是json的字符串，传一个json字符串就行
，当然应该记得在调用的方法中添加引号。要是参数是json串，这就不是字符串，而是使用json转换成的串。
明显的区别是在url的转换不一样。

json串  "{"rows":[{"content":"<p>\t&nbsp;</p><p>\t&nbsp;</p><p style=\"text-align: start; outline: transparent solid 0px; -webkit-touch-callout: none; margin: 0px 0px 20px; word-break: break-word;\">12323</p>","create_date":"2016-03-01 08:56","create_time":"1456793770","id":"5670"}]}"

json的字符串 “{"rows":[{"content":"\u003cp\u003e\t\u0026nbsp;\u003c/p\u003e\u003cp\u003e\t\u0026nbsp;\u003c/p\u003e\u003cp style\u003d\"text-align: start; outline: transparent solid 0px; -webkit-touch-callout: none; margin: 0px 0px 20px; word-break: break-word;\"\u003e12323\u003c/p\u003e","create_date":"2016-03-01 08:56","create_time":"1456793770","id":"5670"}]}”

有差别的。