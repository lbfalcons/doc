android 4.4的打印框架

整体说明

框架整体分为三层，PrintManager，PrintManagerService,PrintService。

PrintManager & PrintManagerService

为app使用的入口。提供了方法print(jobName,printJobAdapter,printJobAttribute)。该api为printjob进入打印框架的入口。app直接调用该api，就完成了操作。打印框架会为app启动一窗口，使用户最后还能修改一次printJobAttribute。排版与重新生成文件的操作由printJobAdapter.onlayout()及printJobAdapter.onWrite()完成。onLayout()与onWrite()完成后，要使用layoutfinish(),writefinish()通知框架，操作完成。

PrintService 打印服务插件

所有的打印服务，以类似插件的形式，注册到系统中。android本身并不包含任何与打印机交互的机制与功能，只是提供了一printservice的接口。类似的打印服务完成操作，框架只负责使用。 生成一个自定义的打印服务，extend printService,并override 所有的方法就可以了。注意，要在配置中，加入打印的相应配置。这样，在服务安装的时候，就可以被PrintManagerService捕获，以完成打印服务的注册。


打印机的识别

识别通过discoverySession完成。PrintService生成一自定义的Session，该session会对PrintService中保存的打印机的状态进行更新。新的打印机，使用PrintService.addPrinter()加入。不在的，使用PrintService.removePrinter()删除。数据都是存储在PrintService中。

这样，框架不用关心具体如何与打印机交互。所有操作都由具体的打印服务插件完成。





资料:
https://developer.android.com/reference/android/print/package-summary.html
https://developer.android.com/reference/android/printservice/PrintService.html
https://developer.android.com/reference/android/printservice/PrinterDiscoverySession.html