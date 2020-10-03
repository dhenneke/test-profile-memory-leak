# test-profile-memory-leak project

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: https://quarkus.io/ .

## Project Details

Shows memory problems when using different Test Profiles.
This project creates 10 Test classes that each use a different Test Profile, and limited the heap space to 64MB.

When I run `./mvnw clean test -Dtest=*` I get the following output.
(This run was on a 1GB 1vCPU cloud Ubuntu VM with AdoptOpenJDK 11.0.8+10 but it also happens on my local windows machine).

```
[INFO] Scanning for projects...
[INFO]
[INFO] -----------------< org.acme:test-profile-memory-leak >------------------
[INFO] Building test-profile-memory-leak 1.0.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ test-profile-memory-leak ---
[INFO] Deleting /root/test-profile-memory-leak/target
[INFO]
[INFO] --- quarkus-maven-plugin:1.8.1.Final:generate-code (default) @ test-profile-memory-leak ---
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ test-profile-memory-leak ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 2 resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:compile (default-compile) @ test-profile-memory-leak ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to /root/test-profile-memory-leak/target/classes
[INFO]
[INFO] --- quarkus-maven-plugin:1.8.1.Final:generate-code-tests (default) @ test-profile-memory-leak ---
[INFO]
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ test-profile-memory-leak ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /root/test-profile-memory-leak/src/test/resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:testCompile (default-testCompile) @ test-profile-memory-leak ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 10 source files to /root/test-profile-memory-leak/target/test-classes
[INFO]
[INFO] --- maven-surefire-plugin:3.0.0-M5:test (default-test) @ test-profile-memory-leak ---
[INFO]
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running org.acme.ExampleResourceTest9
2020-10-03 13:02:03,021 INFO  [io.quarkus] (main) Quarkus 1.8.1.Final on JVM started in 4.433s. Listening on: http://0.0.0.0:8081
2020-10-03 13:02:03,023 INFO  [io.quarkus] (main) Profile test activated.
2020-10-03 13:02:03,024 INFO  [io.quarkus] (main) Installed features: [cdi, resteasy]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 13.126 s - in org.acme.ExampleResourceTest9
[INFO] Running org.acme.ExampleResourceTest4
2020-10-03 13:02:06,876 INFO  [io.quarkus] (main) Quarkus stopped in 0.081s
2020-10-03 13:02:13,344 INFO  [io.quarkus] (main) Quarkus 1.8.1.Final on JVM started in 5.832s. Listening on: http://0.0.0.0:8081
2020-10-03 13:02:13,345 INFO  [io.quarkus] (main) Profile test activated.
2020-10-03 13:02:13,345 INFO  [io.quarkus] (main) Installed features: [cdi, resteasy]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 11.301 s - in org.acme.ExampleResourceTest4
[INFO] Running org.acme.ExampleResourceTest2
2020-10-03 13:02:18,192 INFO  [io.quarkus] (main) Quarkus stopped in 0.073s
[ERROR] Tests run: 1, Failures: 0, Errors: 1, Skipped: 0, Time elapsed: 15.375 s <<< FAILURE! - in org.acme.ExampleResourceTest2
[ERROR] org.acme.ExampleResourceTest2.testHelloEndpoint  Time elapsed: 0.003 s  <<< ERROR!
java.lang.RuntimeException:
java.lang.RuntimeException: io.quarkus.builder.BuildException: Build failure: Build failed due to errors
        [error]: Build step io.quarkus.deployment.steps.ConfigGenerationBuildStep#generateConfigClass threw an exception: java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at io.quarkus.gizmo.BytecodeCreatorImpl$Operation.doProcess(BytecodeCreatorImpl.java:1252)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeInteriorOperations(BytecodeCreatorImpl.java:1145)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeOperations(BytecodeCreatorImpl.java:1139)
        at io.quarkus.gizmo.MethodCreatorImpl.write(MethodCreatorImpl.java:103)
        at io.quarkus.gizmo.ClassCreator.writeTo(ClassCreator.java:180)
        at io.quarkus.gizmo.ClassCreator.close(ClassCreator.java:203)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator$GenerateOperation.run(RunTimeConfigurationGenerator.java:767)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator.generate(RunTimeConfigurationGenerator.java:249)
        at io.quarkus.deployment.steps.ConfigGenerationBuildStep.generateConfigClass(ConfigGenerationBuildStep.java:62)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:936)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at org.jboss.threads.ContextClassLoaderSavingRunnable.run(ContextClassLoaderSavingRunnable.java:35)
        at org.jboss.threads.EnhancedQueueExecutor.safeRun(EnhancedQueueExecutor.java:2046)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.doRunTask(EnhancedQueueExecutor.java:1578)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1452)
        at java.base/java.lang.Thread.run(Thread.java:834)
        at org.jboss.threads.JBossThread.run(JBossThread.java:479)
Caused by: java.lang.OutOfMemoryError: Java heap space
        at java.base/java.util.Arrays.copyOf(Arrays.java:3745)
        at java.base/java.lang.AbstractStringBuilder.ensureCapacityInternal(AbstractStringBuilder.java:172)
        at java.base/java.lang.AbstractStringBuilder.append(AbstractStringBuilder.java:538)
        at java.base/java.lang.StringBuilder.append(StringBuilder.java:174)
        at io.quarkus.gizmo.BytecodeCreatorImpl$InvokeOperation.writeBytecode(BytecodeCreatorImpl.java:1349)
        at io.quarkus.gizmo.BytecodeCreatorImpl$Operation.doProcess(BytecodeCreatorImpl.java:1249)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeInteriorOperations(BytecodeCreatorImpl.java:1145)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeOperations(BytecodeCreatorImpl.java:1139)
        at io.quarkus.gizmo.MethodCreatorImpl.write(MethodCreatorImpl.java:103)
        at io.quarkus.gizmo.ClassCreator.writeTo(ClassCreator.java:180)
        at io.quarkus.gizmo.ClassCreator.close(ClassCreator.java:203)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator$GenerateOperation.run(RunTimeConfigurationGenerator.java:767)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator.generate(RunTimeConfigurationGenerator.java:249)
        at io.quarkus.deployment.steps.ConfigGenerationBuildStep.generateConfigClass(ConfigGenerationBuildStep.java:62)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:936)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at io.quarkus.builder.BuildContext$$Lambda$1489/0x00000001005f8440.run(Unknown Source)
        ... 6 more

Caused by: java.lang.RuntimeException:
io.quarkus.builder.BuildException: Build failure: Build failed due to errors
        [error]: Build step io.quarkus.deployment.steps.ConfigGenerationBuildStep#generateConfigClass threw an exception: java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at io.quarkus.gizmo.BytecodeCreatorImpl$Operation.doProcess(BytecodeCreatorImpl.java:1252)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeInteriorOperations(BytecodeCreatorImpl.java:1145)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeOperations(BytecodeCreatorImpl.java:1139)
        at io.quarkus.gizmo.MethodCreatorImpl.write(MethodCreatorImpl.java:103)
        at io.quarkus.gizmo.ClassCreator.writeTo(ClassCreator.java:180)
        at io.quarkus.gizmo.ClassCreator.close(ClassCreator.java:203)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator$GenerateOperation.run(RunTimeConfigurationGenerator.java:767)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator.generate(RunTimeConfigurationGenerator.java:249)
        at io.quarkus.deployment.steps.ConfigGenerationBuildStep.generateConfigClass(ConfigGenerationBuildStep.java:62)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:936)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at org.jboss.threads.ContextClassLoaderSavingRunnable.run(ContextClassLoaderSavingRunnable.java:35)
        at org.jboss.threads.EnhancedQueueExecutor.safeRun(EnhancedQueueExecutor.java:2046)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.doRunTask(EnhancedQueueExecutor.java:1578)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1452)
        at java.base/java.lang.Thread.run(Thread.java:834)
        at org.jboss.threads.JBossThread.run(JBossThread.java:479)
Caused by: java.lang.OutOfMemoryError: Java heap space
        at java.base/java.util.Arrays.copyOf(Arrays.java:3745)
        at java.base/java.lang.AbstractStringBuilder.ensureCapacityInternal(AbstractStringBuilder.java:172)
        at java.base/java.lang.AbstractStringBuilder.append(AbstractStringBuilder.java:538)
        at java.base/java.lang.StringBuilder.append(StringBuilder.java:174)
        at io.quarkus.gizmo.BytecodeCreatorImpl$InvokeOperation.writeBytecode(BytecodeCreatorImpl.java:1349)
        at io.quarkus.gizmo.BytecodeCreatorImpl$Operation.doProcess(BytecodeCreatorImpl.java:1249)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeInteriorOperations(BytecodeCreatorImpl.java:1145)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeOperations(BytecodeCreatorImpl.java:1139)
        at io.quarkus.gizmo.MethodCreatorImpl.write(MethodCreatorImpl.java:103)
        at io.quarkus.gizmo.ClassCreator.writeTo(ClassCreator.java:180)
        at io.quarkus.gizmo.ClassCreator.close(ClassCreator.java:203)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator$GenerateOperation.run(RunTimeConfigurationGenerator.java:767)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator.generate(RunTimeConfigurationGenerator.java:249)
        at io.quarkus.deployment.steps.ConfigGenerationBuildStep.generateConfigClass(ConfigGenerationBuildStep.java:62)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:936)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at io.quarkus.builder.BuildContext$$Lambda$1489/0x00000001005f8440.run(Unknown Source)
        ... 6 more

Caused by: io.quarkus.builder.BuildException:
Build failure: Build failed due to errors
        [error]: Build step io.quarkus.deployment.steps.ConfigGenerationBuildStep#generateConfigClass threw an exception: java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at io.quarkus.gizmo.BytecodeCreatorImpl$Operation.doProcess(BytecodeCreatorImpl.java:1252)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeInteriorOperations(BytecodeCreatorImpl.java:1145)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeOperations(BytecodeCreatorImpl.java:1139)
        at io.quarkus.gizmo.MethodCreatorImpl.write(MethodCreatorImpl.java:103)
        at io.quarkus.gizmo.ClassCreator.writeTo(ClassCreator.java:180)
        at io.quarkus.gizmo.ClassCreator.close(ClassCreator.java:203)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator$GenerateOperation.run(RunTimeConfigurationGenerator.java:767)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator.generate(RunTimeConfigurationGenerator.java:249)
        at io.quarkus.deployment.steps.ConfigGenerationBuildStep.generateConfigClass(ConfigGenerationBuildStep.java:62)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:936)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at org.jboss.threads.ContextClassLoaderSavingRunnable.run(ContextClassLoaderSavingRunnable.java:35)
        at org.jboss.threads.EnhancedQueueExecutor.safeRun(EnhancedQueueExecutor.java:2046)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.doRunTask(EnhancedQueueExecutor.java:1578)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1452)
        at java.base/java.lang.Thread.run(Thread.java:834)
        at org.jboss.threads.JBossThread.run(JBossThread.java:479)
Caused by: java.lang.OutOfMemoryError: Java heap space
        at java.base/java.util.Arrays.copyOf(Arrays.java:3745)
        at java.base/java.lang.AbstractStringBuilder.ensureCapacityInternal(AbstractStringBuilder.java:172)
        at java.base/java.lang.AbstractStringBuilder.append(AbstractStringBuilder.java:538)
        at java.base/java.lang.StringBuilder.append(StringBuilder.java:174)
        at io.quarkus.gizmo.BytecodeCreatorImpl$InvokeOperation.writeBytecode(BytecodeCreatorImpl.java:1349)
        at io.quarkus.gizmo.BytecodeCreatorImpl$Operation.doProcess(BytecodeCreatorImpl.java:1249)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeInteriorOperations(BytecodeCreatorImpl.java:1145)
        at io.quarkus.gizmo.BytecodeCreatorImpl.writeOperations(BytecodeCreatorImpl.java:1139)
        at io.quarkus.gizmo.MethodCreatorImpl.write(MethodCreatorImpl.java:103)
        at io.quarkus.gizmo.ClassCreator.writeTo(ClassCreator.java:180)
        at io.quarkus.gizmo.ClassCreator.close(ClassCreator.java:203)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator$GenerateOperation.run(RunTimeConfigurationGenerator.java:767)
        at io.quarkus.deployment.configuration.RunTimeConfigurationGenerator.generate(RunTimeConfigurationGenerator.java:249)
        at io.quarkus.deployment.steps.ConfigGenerationBuildStep.generateConfigClass(ConfigGenerationBuildStep.java:62)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:936)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at io.quarkus.builder.BuildContext$$Lambda$1489/0x00000001005f8440.run(Unknown Source)
        ... 6 more

Caused by: java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
Caused by: java.lang.OutOfMemoryError: Java heap space

[INFO] Running org.acme.ExampleResourceTest7
[ERROR] Tests run: 1, Failures: 0, Errors: 1, Skipped: 0, Time elapsed: 14.305 s <<< FAILURE! - in org.acme.ExampleResourceTest7
[ERROR] org.acme.ExampleResourceTest7.testHelloEndpoint  Time elapsed: 0.168 s  <<< ERROR!
java.lang.RuntimeException:
java.lang.RuntimeException: io.quarkus.builder.BuildException: Build failure: Build failed due to errors
        [error]: Build step io.quarkus.deployment.index.ApplicationArchiveBuildStep#build threw an exception: java.lang.OutOfMemoryError: Java heap space
        at jdk.zipfs/jdk.nio.zipfs.ZipFileSystem.initCEN(ZipFileSystem.java:1099)
        at jdk.zipfs/jdk.nio.zipfs.ZipFileSystem.<init>(ZipFileSystem.java:130)
        at jdk.zipfs/jdk.nio.zipfs.ZipFileSystemProvider.newFileSystem(ZipFileSystemProvider.java:136)
        at java.base/java.nio.file.FileSystems.newFileSystem(FileSystems.java:406)
        at io.quarkus.deployment.index.ApplicationArchiveBuildStep.addMarkerFilePaths(ApplicationArchiveBuildStep.java:211)
        at io.quarkus.deployment.index.ApplicationArchiveBuildStep.scanForOtherIndexes(ApplicationArchiveBuildStep.java:129)
        at io.quarkus.deployment.index.ApplicationArchiveBuildStep.build(ApplicationArchiveBuildStep.java:107)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:936)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at io.quarkus.builder.BuildContext$$Lambda$1657/0x0000000100afd440.run(Unknown Source)
        at org.jboss.threads.ContextClassLoaderSavingRunnable.run(ContextClassLoaderSavingRunnable.java:35)
        at org.jboss.threads.EnhancedQueueExecutor.safeRun(EnhancedQueueExecutor.java:2046)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.doRunTask(EnhancedQueueExecutor.java:1578)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1452)
        at java.base/java.lang.Thread.run(Thread.java:834)
        at org.jboss.threads.JBossThread.run(JBossThread.java:479)

Caused by: java.lang.RuntimeException:
io.quarkus.builder.BuildException: Build failure: Build failed due to errors
        [error]: Build step io.quarkus.deployment.index.ApplicationArchiveBuildStep#build threw an exception: java.lang.OutOfMemoryError: Java heap space
        at jdk.zipfs/jdk.nio.zipfs.ZipFileSystem.initCEN(ZipFileSystem.java:1099)
        at jdk.zipfs/jdk.nio.zipfs.ZipFileSystem.<init>(ZipFileSystem.java:130)
        at jdk.zipfs/jdk.nio.zipfs.ZipFileSystemProvider.newFileSystem(ZipFileSystemProvider.java:136)
        at java.base/java.nio.file.FileSystems.newFileSystem(FileSystems.java:406)
        at io.quarkus.deployment.index.ApplicationArchiveBuildStep.addMarkerFilePaths(ApplicationArchiveBuildStep.java:211)
        at io.quarkus.deployment.index.ApplicationArchiveBuildStep.scanForOtherIndexes(ApplicationArchiveBuildStep.java:129)
        at io.quarkus.deployment.index.ApplicationArchiveBuildStep.build(ApplicationArchiveBuildStep.java:107)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:936)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at io.quarkus.builder.BuildContext$$Lambda$1657/0x0000000100afd440.run(Unknown Source)
        at org.jboss.threads.ContextClassLoaderSavingRunnable.run(ContextClassLoaderSavingRunnable.java:35)
        at org.jboss.threads.EnhancedQueueExecutor.safeRun(EnhancedQueueExecutor.java:2046)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.doRunTask(EnhancedQueueExecutor.java:1578)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1452)
        at java.base/java.lang.Thread.run(Thread.java:834)
        at org.jboss.threads.JBossThread.run(JBossThread.java:479)

Caused by: io.quarkus.builder.BuildException:
Build failure: Build failed due to errors
        [error]: Build step io.quarkus.deployment.index.ApplicationArchiveBuildStep#build threw an exception: java.lang.OutOfMemoryError: Java heap space
        at jdk.zipfs/jdk.nio.zipfs.ZipFileSystem.initCEN(ZipFileSystem.java:1099)
        at jdk.zipfs/jdk.nio.zipfs.ZipFileSystem.<init>(ZipFileSystem.java:130)
        at jdk.zipfs/jdk.nio.zipfs.ZipFileSystemProvider.newFileSystem(ZipFileSystemProvider.java:136)
        at java.base/java.nio.file.FileSystems.newFileSystem(FileSystems.java:406)
        at io.quarkus.deployment.index.ApplicationArchiveBuildStep.addMarkerFilePaths(ApplicationArchiveBuildStep.java:211)
        at io.quarkus.deployment.index.ApplicationArchiveBuildStep.scanForOtherIndexes(ApplicationArchiveBuildStep.java:129)
        at io.quarkus.deployment.index.ApplicationArchiveBuildStep.build(ApplicationArchiveBuildStep.java:107)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:936)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at io.quarkus.builder.BuildContext$$Lambda$1657/0x0000000100afd440.run(Unknown Source)
        at org.jboss.threads.ContextClassLoaderSavingRunnable.run(ContextClassLoaderSavingRunnable.java:35)
        at org.jboss.threads.EnhancedQueueExecutor.safeRun(EnhancedQueueExecutor.java:2046)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.doRunTask(EnhancedQueueExecutor.java:1578)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1452)
        at java.base/java.lang.Thread.run(Thread.java:834)
        at org.jboss.threads.JBossThread.run(JBossThread.java:479)

Caused by: java.lang.OutOfMemoryError: Java heap space

[INFO] Running org.acme.ExampleResourceTest10
[ERROR] Tests run: 1, Failures: 0, Errors: 1, Skipped: 0, Time elapsed: 4.483 s <<< FAILURE! - in org.acme.ExampleResourceTest10
[ERROR] org.acme.ExampleResourceTest10.testHelloEndpoint  Time elapsed: 0.005 s  <<< ERROR!
java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
Caused by: java.lang.OutOfMemoryError: Java heap space

[INFO] Running org.acme.ExampleResourceTest8
[ERROR] Tests run: 1, Failures: 0, Errors: 1, Skipped: 0, Time elapsed: 4.085 s <<< FAILURE! - in org.acme.ExampleResourceTest8
[ERROR] org.acme.ExampleResourceTest8.testHelloEndpoint  Time elapsed: 0.003 s  <<< ERROR!
java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
Caused by: java.lang.OutOfMemoryError: Java heap space

[INFO] Running org.acme.ExampleResourceTest3
[ERROR] Tests run: 1, Failures: 0, Errors: 1, Skipped: 0, Time elapsed: 4.313 s <<< FAILURE! - in org.acme.ExampleResourceTest3
[ERROR] org.acme.ExampleResourceTest3.testHelloEndpoint  Time elapsed: 0.004 s  <<< ERROR!
java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
Caused by: java.lang.OutOfMemoryError: Java heap space

[INFO] Running org.acme.ExampleResourceTest6
[ERROR] Tests run: 1, Failures: 0, Errors: 1, Skipped: 0, Time elapsed: 4.188 s <<< FAILURE! - in org.acme.ExampleResourceTest6
[ERROR] org.acme.ExampleResourceTest6.testHelloEndpoint  Time elapsed: 0.005 s  <<< ERROR!
java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
Caused by: java.lang.OutOfMemoryError: Java heap space

[INFO] Running org.acme.ExampleResourceTest5
[ERROR] Tests run: 1, Failures: 0, Errors: 1, Skipped: 0, Time elapsed: 4.064 s <<< FAILURE! - in org.acme.ExampleResourceTest5
[ERROR] org.acme.ExampleResourceTest5.testHelloEndpoint  Time elapsed: 0.009 s  <<< ERROR!
java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
Caused by: java.lang.OutOfMemoryError: Java heap space

[INFO] Running org.acme.ExampleResourceTest1
[ERROR] Tests run: 1, Failures: 0, Errors: 1, Skipped: 0, Time elapsed: 2.905 s <<< FAILURE! - in org.acme.ExampleResourceTest1
[ERROR] org.acme.ExampleResourceTest1.testHelloEndpoint  Time elapsed: 0.149 s  <<< ERROR!
java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
Caused by: java.lang.OutOfMemoryError: Java heap space

[INFO]
[INFO] Results:
[INFO]
[ERROR] Errors:
[ERROR]   ExampleResourceTest1.testHelloEndpoint » Runtime java.lang.OutOfMemoryError: J...
[ERROR]   ExampleResourceTest10.testHelloEndpoint » Runtime java.lang.OutOfMemoryError: ...
[ERROR]   ExampleResourceTest2.testHelloEndpoint » Runtime java.lang.RuntimeException: i...
[ERROR]   ExampleResourceTest3.testHelloEndpoint » Runtime java.lang.OutOfMemoryError: J...
[ERROR]   ExampleResourceTest5.testHelloEndpoint » Runtime java.lang.OutOfMemoryError: J...
[ERROR]   ExampleResourceTest6.testHelloEndpoint » Runtime java.lang.OutOfMemoryError: J...
[ERROR]   ExampleResourceTest7.testHelloEndpoint » Runtime java.lang.RuntimeException: i...
[ERROR]   ExampleResourceTest8.testHelloEndpoint » Runtime java.lang.OutOfMemoryError: J...
[INFO]
[ERROR] Tests run: 10, Failures: 0, Errors: 8, Skipped: 0
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  01:30 min
[INFO] Finished at: 2020-10-03T13:03:12Z
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:3.0.0-M5:test (default-test) on project test-profile-memory-leak: There are test failures.
[ERROR]
[ERROR] Please refer to /root/test-profile-memory-leak/target/surefire-reports for the individual test results.
[ERROR] Please refer to dump files (if any exist) [date].dump, [date]-jvmRun[N].dump and [date].dumpstream.
[ERROR] -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoFailureException
```  

Heap space was limited to `-Xmx64m`, though it also happens with `-Xmx128m` (just with more tests executed correctly).
