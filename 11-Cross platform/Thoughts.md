# 演进路线图

![[Pasted image 20251112221819.png]]![[Pasted image 20251112222321.png]]
# 阶段性原理解释：

## webView & JSBridge：
![[Pasted image 20251113220225.png]]
这里以`Android`系统为例：
### 前端调用原生能力：
- 打开 JS：`webView.getSettings().setJavaScriptEnabled(true)`；
- 定义一个 Java/Kotlin 类，并在需要暴露给 JS 的方法上标注 `@JavasriptInterface`；
- 通过 `webView.addJavascriptInterface(instance, "namespace")` 将方法注入到`webview`中；
- 前端即可通过 `window.namespace.method(args)` 调用到对应原生方法。
==**原生方法是以对象属性形式挂载在全局的window对象下的。**==
### 原生调用前端：
- `webview.loadUrl("")`
- `webview.evaluateJavascript(javaScriptString, callBack)`
效果上相当于在浏览器的控制台执行了一段js代码。
---
# flutter
![[Pasted image 20251113225256.png]]