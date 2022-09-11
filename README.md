# mvnd-jetty-plugin-issue
Example project using jetty-maven-plugin to show class loading issue when using mvnd (versus mvn).

`mvn clean install` - builds and tests the project

`mvnd clean install` - builds and attempts to test; encounters the following exception on jetty startup:

```
java.lang.NoClassDefFoundError: javax/servlet/ServletContainerInitializer
	at java.base/java.lang.ClassLoader.defineClass1(Native Method)
	at java.base/java.lang.ClassLoader.defineClass(ClassLoader.java:1012)
	at java.base/java.security.SecureClassLoader.defineClass(SecureClassLoader.java:150)
	at java.base/java.net.URLClassLoader.defineClass(URLClassLoader.java:524)
	at java.base/java.net.URLClassLoader$1.run(URLClassLoader.java:427)
	at java.base/java.net.URLClassLoader$1.run(URLClassLoader.java:421)
	at java.base/java.security.AccessController.doPrivileged(AccessController.java:712)
	at java.base/java.net.URLClassLoader.findClass(URLClassLoader.java:420)
	at org.mvndaemon.mvnd.common.MavenDaemon$1.findClass(MavenDaemon.java:62)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:587)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:520)
	at org.codehaus.plexus.classworlds.realm.ClassRealm.loadClassFromParent(ClassRealm.java:469)
	at org.codehaus.plexus.classworlds.strategy.SelfFirstStrategy.loadClass(SelfFirstStrategy.java:46)
	at org.codehaus.plexus.classworlds.realm.ClassRealm.unsynchronizedLoadClass(ClassRealm.java:271)
	at org.codehaus.plexus.classworlds.realm.ClassRealm.loadClass(ClassRealm.java:247)
	at org.codehaus.plexus.classworlds.realm.ClassRealm.loadClass(ClassRealm.java:239)
	at org.eclipse.jetty.webapp.WebAppClassLoader.loadClass(WebAppClassLoader.java:538)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:520)
	at java.base/java.lang.Class.forName0(Native Method)
	at java.base/java.lang.Class.forName(Class.java:467)
	at java.base/java.util.ServiceLoader$LazyClassPathLookupIterator.nextProviderClass(ServiceLoader.java:1217)
	at java.base/java.util.ServiceLoader$LazyClassPathLookupIterator.hasNextService(ServiceLoader.java:1228)
	at java.base/java.util.ServiceLoader$LazyClassPathLookupIterator.hasNext(ServiceLoader.java:1273)
	at java.base/java.util.ServiceLoader$2.hasNext(ServiceLoader.java:1309)
	at java.base/java.util.ServiceLoader$3.hasNext(ServiceLoader.java:1393)
	at org.eclipse.jetty.annotations.AnnotationConfiguration.getNonExcludedInitializers(AnnotationConfiguration.java:829)
	at org.eclipse.jetty.annotations.AnnotationConfiguration.configure(AnnotationConfiguration.java:343)
	at org.eclipse.jetty.webapp.WebAppContext.configure(WebAppContext.java:498)
	at org.eclipse.jetty.webapp.WebAppContext.startContext(WebAppContext.java:1409)
	at org.eclipse.jetty.server.handler.ContextHandler.doStart(ContextHandler.java:916)
	at org.eclipse.jetty.servlet.ServletContextHandler.doStart(ServletContextHandler.java:288)
	at org.eclipse.jetty.webapp.WebAppContext.doStart(WebAppContext.java:524)
	at org.eclipse.jetty.maven.plugin.JettyWebAppContext.doStart(JettyWebAppContext.java:397)
	at org.eclipse.jetty.util.component.AbstractLifeCycle.start(AbstractLifeCycle.java:73)
	at org.eclipse.jetty.util.component.ContainerLifeCycle.start(ContainerLifeCycle.java:169)
	at org.eclipse.jetty.util.component.ContainerLifeCycle.doStart(ContainerLifeCycle.java:117)
	at org.eclipse.jetty.server.handler.AbstractHandler.doStart(AbstractHandler.java:97)
	at org.eclipse.jetty.util.component.AbstractLifeCycle.start(AbstractLifeCycle.java:73)
	at org.eclipse.jetty.util.component.ContainerLifeCycle.start(ContainerLifeCycle.java:169)
	at org.eclipse.jetty.util.component.ContainerLifeCycle.doStart(ContainerLifeCycle.java:117)
	at org.eclipse.jetty.server.handler.AbstractHandler.doStart(AbstractHandler.java:97)
	at org.eclipse.jetty.util.component.AbstractLifeCycle.start(AbstractLifeCycle.java:73)
	at org.eclipse.jetty.util.component.ContainerLifeCycle.start(ContainerLifeCycle.java:169)
	at org.eclipse.jetty.server.Server.start(Server.java:423)
	at org.eclipse.jetty.util.component.ContainerLifeCycle.doStart(ContainerLifeCycle.java:110)
	at org.eclipse.jetty.server.handler.AbstractHandler.doStart(AbstractHandler.java:97)
	at org.eclipse.jetty.server.Server.doStart(Server.java:387)
	at org.eclipse.jetty.util.component.AbstractLifeCycle.start(AbstractLifeCycle.java:73)
	at org.eclipse.jetty.maven.plugin.AbstractJettyMojo.startJetty(AbstractJettyMojo.java:449)
	at org.eclipse.jetty.maven.plugin.AbstractJettyMojo.execute(AbstractJettyMojo.java:310)
	at org.eclipse.jetty.maven.plugin.JettyRunMojo.execute(JettyRunMojo.java:150)
	at org.eclipse.jetty.maven.plugin.JettyStartMojo.execute(JettyStartMojo.java:50)
	at org.apache.maven.plugin.DefaultBuildPluginManager.executeMojo(DefaultBuildPluginManager.java:137)
	at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute(MojoExecutor.java:301)
	at org.apache.maven.lifecycle.internal.MojoExecutor.execute(MojoExecutor.java:211)
	at org.apache.maven.lifecycle.internal.MojoExecutor.execute(MojoExecutor.java:165)
	at org.apache.maven.lifecycle.internal.MojoExecutor.execute(MojoExecutor.java:157)
	at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject(LifecycleModuleBuilder.java:121)
	at org.mvndaemon.mvnd.builder.SmartBuilderImpl.buildProject(SmartBuilderImpl.java:178)
	at org.mvndaemon.mvnd.builder.SmartBuilderImpl$ProjectBuildTask.run(SmartBuilderImpl.java:198)
	at java.base/java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:539)
	at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:264)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1136)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:635)
	at java.base/java.lang.Thread.run(Thread.java:833)
Caused by: java.lang.ClassNotFoundException: javax.servlet.ServletContainerInitializer
	at java.base/jdk.internal.loader.BuiltinClassLoader.loadClass(BuiltinClassLoader.java:641)
	at java.base/jdk.internal.loader.ClassLoaders$AppClassLoader.loadClass(ClassLoaders.java:188)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:520)
	at org.mvndaemon.mvnd.common.MavenDaemon$1.findClass(MavenDaemon.java:64)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:587)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:520)
	... 65 common frames omitted

Version info:
```
mvnd 0.8.0 darwin-amd64 native client (2cfffe23eebac7a0fddecf0268478ae963a8859f)
Terminal: org.jline.terminal.impl.PosixSysTerminal with pty org.jline.terminal.impl.jansi.osx.OsXNativePty
Apache Maven 3.8.5 (3599d3414f046de2324203b78ddcf9b5e4388aa0)
Maven home: /usr/local/Cellar/mvnd/0.8.0/libexec/mvn
Java version: 17.0.3, vendor: Azul Systems, Inc., runtime: /Library/Java/JavaVirtualMachines/zulu-17.jdk/Contents/Home
Default locale: en_US, platform encoding: UTF-8
OS name: "mac os x", version: "12.5.1", arch: "x86_64", family: "mac"
```
