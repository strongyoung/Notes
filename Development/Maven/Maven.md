#

打包成可执行有主类的jar包
---

``
<project>
  ...
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        ...
        <configuration>
          <archive>
            <manifest>
              <addClasspath>true</addClasspath>
              <mainClass>fully.qualified.MainClass</mainClass> <!-- 你的主类名 -->
            </manifest>
          </archive>
        </configuration>
        ...
      </plugin>
    </plugins>
  </build>
```
But, 虽然现在把程序打包成了jar文件，也可以运行，但是，这个jar包是没有包含依赖的，因此，如果这个程序有其他依赖，那么在运行这个程序的时候，需要指定类目录，并且要把所有的依赖都放到类目录下去，手动添加依赖到类目录下，简直就是恶梦。。。

我曾经就这么干过，它少一个依赖，我就手动加一个到类目录，少一个，加一个，少一个，加一个，当我加了大概有10几个之后，而且还看不到尽头。。。简直要疯的节奏，然后想起之前用sbt打包，也是可以把依赖添加到jar包，心情顿时好转，赶紧google，于是找到google到了maven的官网...。顺便说一下，虽然我们google的时候，会搜索到很多结果，但很多时候，我们最好选择合适的结果进行阅读，我的一般顺序是：官方优先，StackExchange。。。

## 配置
编辑pom.xml文件，内容如下：
```
<project>
  [...]
  <build>
    [...]
    <plugins>
      <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <version>3.0.0</version>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
        <executions>
          <execution>
            <id>make-assembly</id> <!-- this is used for inheritance merges -->
            <phase>package</phase> <!-- bind to the packaging phase -->
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
      [...]
</project>
```

## 打包 
使用以下命令打包：
```
mvn package
```

就像官方网站说的，" this is pretty simple! "

参考文献：

[1] https://maven.apache.org/plugins/maven-assembly-plugin/usage.html