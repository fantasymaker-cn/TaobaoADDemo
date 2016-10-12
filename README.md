# 仿淘宝闪屏广告

淘宝在从后台切换回前台时, 会出现一个3秒钟的广告页面. 但不是每次都有, 估计进行了时间间隔判断或者其他判断. 实现这个功能很简单, 要点主要是:

1. 后台恢复到前台的判断
2. 无论之前在哪个页面, 从后台切换回来都能够出现广告页
3. 短时间内反复前后台切换, 根据时间间隔判断是否出现广告页
4. 广告页面倒计时3秒后消失

以上3点需求, 分别可以用以下方案解决:

1. 后台恢复到前台的判断
在Application中注册ActivityLifecycleCallbacks(API 14), 监听所有Activity的onStart()和onStop(). 当所有Activity都onStop()时, 即为后台, 记录前台可见Activity数量为0; 当数量从0增加到非0时, 即为前台
2. 无论之前在哪个页面, 从后台切换回来都能够出现广告页
在Activity基类的onStart()中实现广告页面的显示
3. 短时间内反复前后台切换, 根据时间间隔判断是否出现广告页
增加一个每次显示广告时当前时间的记录, 下次显示广告前先判断当前时间与上次时间间隔是否达到. 
4. 广告页面倒计时3秒后消失
使用简单的CountDownTimer实现倒计时

详细内容: [淘宝后台恢复闪屏广告的实现](http://blog.fantasymaker.cn/2016/10/12/android-taobao-ad-screen/)


## 效果

![Gif](http://7xnm3h.com1.z0.glb.clouddn.com/gif/taobao-ad.gif)