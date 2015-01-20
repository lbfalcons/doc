android 4.4的打印框架

编程api

框架提供了api，PrintManager.print(jobname，PrintjobAdapter,PrintAttribute)，该api会触发一配置窗口，完成具体的打印配置的操作，也是对api传入的PrintAttribute的最后一次修正机会。 App调用该api，以及在窗口操作时，点击打印按钮就可以了。此流程与windows上的打印文件方式类似，但无法完成api调用后，自动完成打印功能。

打印服务

所有的打印服务，以类似插件的形式，注册到系统中。android本身并不包含任何与打印机交互的机制与功能，只是提供了一printservice的接口。类似的打印服务完成操作，框架只负责使用。


打印机的识别

PrintManager有一发现线程，完成打印机的发现操作，但具体的操作还是由打印服务完成的。线程只是调用。





资料:
https://developer.android.com/reference/android/print/package-summary.html
https://developer.android.com/reference/android/printservice/PrintService.html