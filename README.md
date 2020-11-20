# -H:IncludeResources stopped working in GraalVM 20.3.0

A reproducer for https://github.com/oracle/graal/issues/3003

## Steps to reproduce:


```
git clone git@github.com:ppalaga/include-resources.git
cd include-resources

# Test with 20.2.0
export JAVA_HOME=~/bin/graalvm/graalvm-ce-java11-20.2.0

$JAVA_HOME/bin/java -version
openjdk version "11.0.8" 2020-07-14
OpenJDK Runtime Environment GraalVM CE 20.2.0 (build 11.0.8+10-jvmci-20.2-b03)
OpenJDK 64-Bit Server VM GraalVM CE 20.2.0 (build 11.0.8+10-jvmci-20.2-b03, mixed mode, sharing)

mvn clean package

./app/target/app # the output is as expected, both resources are there in the image
app/app-resource.txt: Hello from the app
module/module-resource.txt: Hello from the module

# Now test with 20.3.0
export JAVA_HOME=~/bin/graalvm/graalvm-ce-java11-20.3.0

$JAVA_HOME/bin/java -version
openjdk version "11.0.9" 2020-10-20
OpenJDK Runtime Environment GraalVM CE 20.3.0 (build 11.0.9+10-jvmci-20.3-b06)
OpenJDK 64-Bit Server VM GraalVM CE 20.3.0 (build 11.0.9+10-jvmci-20.3-b06, mixed mode, sharing)

mvn clean package

./app/target/app # the output is not OK, none of the resources is there in the image
app/app-resource.txt not available
module/module-resource.txt not available
```

