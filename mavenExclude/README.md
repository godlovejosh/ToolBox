有时，你以为解决了，但是偏偏还是报类包冲突（典型症状是java.lang.ClassNotFoundException或Method不兼容等异常），这时你可以设置一个断点，在断点处通过下面这个我做的工具类来查看Class所来源的JAR包。

随便写一个测试，设置好断点，在执行到断点处按alt+F8动态执行代码（intelij idea），假设我们输入：
ClassLocationUtils.where(org.objectweb.asm.ClassVisitor.class)  
即可马上查出类对应的JAR了：

这就是org.objectweb.asm.ClassVisitor类在运行期对应的JAR包，如果这个JAR包版本不是你期望你，就说明是你的IDE缓存造成的，这时建议你Reimport一下maven列表就可以了，如下所示(idea)：

Reimport一下，IDE会强制根据新的pom.xml设置重新分析并加载依赖类包，以得到和pom.xml设置相同的依赖。（这一步非常重要哦，经常项目组pom.xml是相同的，但是就是有些人可以运行，有些人不能运行，俗称人品问题，其实都是IDE的缓存造成的了
idea清除缓存,为了提高效率不建议采用reimport重新起开启项目的方式,建议采用idea自带的功能,File->Invalidate Caches 功能直接完成清除idea cache

