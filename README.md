To reproduce, install the distribution:

```
./gradlew installDist
cd build/install/okhttp3-appcds-issue/bin
```

Generate archive:
```
JAVA_HOME=<path-to-jdk-17.0.3> JAVA_OPTS=-XX:ArchiveClassesAtExit=okhttp3-appcds-issue.jsa ./okhttp3-appcds-issue
```

Start the application with the archive:
```
JAVA_HOME=<path-to-jdk-17.0.3> JAVA_OPTS=-XX:SharedArchiveFile=okhttp3-appcds-issue.jsa ./okhttp3-appcds-issue
```

Note the failure:
```
Exception in thread "main" java.lang.VerifyError: Bad type on operand stack
Exception Details:
  Location:
    okhttp3/internal/Util
  Reason:
    Type '[Ljava/lang/Object;' is not assignable to 'okhttp3/internal/Util'

	at okhttp3.internal.concurrent.TaskRunner.<clinit>(TaskRunner.kt:309)
	at okhttp3.ConnectionPool.<init>(ConnectionPool.kt:41)
	at okhttp3.ConnectionPool.<init>(ConnectionPool.kt:47)
	at okhttp3.OkHttpClient$B
```
