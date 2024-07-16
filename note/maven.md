# Maven快速入门

## Maven简介

Maven是一个项目管理工具。它负责管理项目开发过程中的几乎所有的东西。

- 版本 - maven 有自己的版本定义和规则。
- 构建 - maven 支持许多种的应用程序类型，对于每一种支持的应用程序类型都定义好了一组构建规则和工具集。
- 输出物管理 - maven 可以管理项目构建的产物，并将其加入到用户库中。这个功能可以用于项目组和其他部门之间的交付行为。
- 依赖关系 - maven 对依赖关系的特性进行细致的分析和划分，避免开发过程中的依赖混乱和相互污染行为
- 文档和构建结果 - maven 的 site 命令支持各种文档信息的发布，包括构建过程的各种输出，javadoc，产品文档等。
- 项目关系 - 一个大型的项目通常有几个小项目或者模块组成，用 maven 可以很方便地管理。
- 移植性管理 - maven 可以针对不同的开发场景，输出不同种类的输出结果。

## Maven标准结构

```xml
|-- pom.xml(maven的核心配置文件)
|-- src
|-- main
  |-- java(java源代码目录)
  |-- resources(资源文件目录)
|-- test
    |-- java(单元测试代码目录)
|-- target(输出目录，所有的输出物都存放在这个目录下)
    |-- classes(编译后的class文件存放处)
```

## Maven的生命周期

一个典型的 Maven 构建（build）生命周期是由以下几个阶段的序列组成的：
![maven生命周期](https://mobsidian.oss-cn-beijing.aliyuncs.com/202407152058806.png)
![阶段](https://mobsidian.oss-cn-beijing.aliyuncs.com/202407152059297.png)

Maven 有以下三个标准的生命周期：

1. **Clean** 生命周期
    - clean：删除目标目录中的编译输出文件。这通常是在构建之前执行的，以确保项目从一个干净的状态开始。

2. **Default** 生命周期（也称为 Build 生命周期）
   - validate：验证项目的正确性，例如检查项目的版本是否正确。
   - compile：编译项目的源代码。
   - test：运行项目的单元测试。
   - package：将编译后的代码打包成可分发的格式，例如 JAR 或 WAR。
   - verify：对项目进行额外的检查以确保质量。
   - install：将项目的构建结果安装到本地 Maven 仓库中，以供其他项目使用。
   - deploy：将项目的构建结果复制到远程仓库，以供其他开发人员或团队使用。
  
3. **Site** 生命周期：
   - site：生成项目文档和站点信息。
   - deploy-site：将生成的站点信息发布到远程服务器，以便共享项目文档。

![goal](https://mobsidian.oss-cn-beijing.aliyuncs.com/202407161952207.png)
其实我们类比一下就明白了：

- lifecycle相当于Java的package，它包含一个或多个phase；
- phase相当于Java的class，它包含一个或多个goal；
- goal相当于class的method，它其实才是真正干活的。

如果我们运行`mvn package`，Maven就会执行default生命周期，它会从开始一直运行到package这个phase为止  
所以，我们使用`mvn`这个命令时，后面的参数是phase，Maven自动根据生命周期运行到指定的phase。

## 依赖管理

```xml
  <dependencies>
    <dependency>
     <groupId>org.apache.maven</groupId>
      <artifactId>maven-embedder</artifactId>
      <version>2.0</version>
      <type>jar</type>
      <scope>test</scope>
      <optional>true</optional>
      <exclusions>
        <exclusion>
          <groupId>org.apache.maven</groupId>
          <artifactId>maven-core</artifactId>
        </exclusion>
      </exclusions>
    </dependency>
    ...
  </dependencies>
  ```

- groupId - 团体、组织的标识符。团体标识的约定是，它以创建这个项目的组织名称的逆向域名(reverse domain name)开头。一般对应着 JAVA 的包的结构。例如 org.apache
- artifactId - 单独项目的唯一标识符。比如我们的 tomcat, commons 等。不要在 artifactId 中包含点号(.)。
- version - 一个项目的特定版本。
- type - 对应 packaging 的类型，如果不使用 type 标签，maven 默认为 jar。
- scope - 此元素指的是任务的类路径（编译和运行时，测试等）以及如何限制依赖关系的传递性。
![](https://mobsidian.oss-cn-beijing.aliyuncs.com/202407152125285.png)
- optional - optional 让其他项目知道，当您使用此项目时，您不需要这种依赖性才能正常工作。
- exclusions - 包含一个或多个排除元素,每个排除元素都包含一个表示要排除的依赖关系的 groupId 和 artifactId。目的是主动断开依赖的资源

maven 支持继承功能。子 POM 可以使用 parent 指定父 POM ，然后继承其配置。
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>my-parent</artifactId>
    <version>2.0</version>
    <relativePath>../my-parent</relativePath>
  </parent>

  <artifactId>my-project</artifactId>
</project>
```

- relativePath - 父项目的pom.xml文件的相对路径。相对路径允许你选择一个不同的路径。默认值是../pom.xml。Maven首先在构建当前项目的地方寻找父项目的pom，其次在文件系统的这个位置（relativePath位置），然后在本地仓库，最后在远程仓库寻找父项目的pom。
  
## dependencyManagement

dependencyManagement 是表示依赖 jar 包的声明。即你在项目中的 dependencyManagement 下声明了依赖，maven 不会加载该依赖，dependencyManagement 声明可以被子 POM 继承。

dependencyManagement 的一个使用案例是当有父子项目的时候，父项目中可以利用 dependencyManagement 声明子项目中需要用到的依赖 jar 包，之后，当某个或者某几个子项目需要加载该依赖的时候，就可以在*子项目*中 dependencies 节点只配置 groupId 和 artifactId 就可以完成依赖的引用，而不需要版本号

dependencyManagement 主要是为了**统一管理依赖包的版本**，确保所有子项目使用的版本一致，类似的还有plugins和pluginManagement。

## modules
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>org.codehaus.mojo</groupId>
  <artifactId>my-parent</artifactId>
  <version>2.0</version>
  <packaging>pom</packaging>

  <modules>
    <module>my-project</module>
    <module>another-project</module>
    <module>third-project/pom-example.xml</module>
  </modules>
</project>
```
用于快速构建maven工程，一次性构建多个模块
制作方式：
1. 创建一个空模块，打包类型为pom
2. 定义其他模块

## properties

```xml
<!--定义自定义属性-->
 <properties>
 <spring.version>5.1.9.RELEASE</spring.version>
 <junit.version>4.12</junit.version>
 </properties>
 ```

 调用方法

 ```xml
 <dependency>
 <groupId>org.springframework</groupId>
 <artifactId>spring-context</artifactId>
 <version>${spring.version}</version>
 </dependency>
 ```

## profile

### profile简介

Maven的Profile用于在不同的环境下应用不同的配置。一套配置即称为一个Profile。这里的“环境”可以是操作系统版本，JDK版本或某些文件是否存在这样的物理环境，也可以是你自己定义的一套逻辑环境。比如上面的A中所说的Linux和Mac OS X便是一种物理环境，而B中讲的开发环境和部署环境则为逻辑环境。Maven提供了Activation机制来激活某个Profile，它既允许自动激活（即在某些条件满足时自动使某个Profile生效），也可以手动激活。
**一个Profile几乎可以包含所有能够出现在pom.xml中的配置项**，比如\<artifactId>，\<outputDirectory>等。相当于在Profile中定义的配置信息会覆盖原有pom.xml中的相应配置项
> [profile](https://www.cnblogs.com/davenkin/p/advanced-maven-use-profile.html)
> [Maven Profile 与 Spring Profile 管理多环境打包](https://lotabout.me/2018/Maven-Profile-and-Spring-Profile/)

```xml
<profiles>
    <profile>
        <id>development</id>
        <properties>
            <environment>dev</environment>
        </properties>
    </profile>
    <profile>
        <id>production</id>
        <properties>
            <environment>prod</environment>
        </properties>
    </profile>
</profiles>
```

### profile的范围

1. pom.xml
pom.xml 中声明的 profile 只对当前项目有效。
2. 用户 settings.xml
在用户目录下的“.m2/settings.xml”中的 profile，对本机上的该用户的所有 Maven 项目有效。
3. 全局 settings.xml
在 Maven 安装目录下 conf/settings.xml 中配置的 profile，对本机上所有项目都有效。

上面三种profile会合并在一块，优先合并全局 settings.xml、再合并用户 settings.xml，最后合并项目的pom.xml. 而且相同的标签以最后一个起作用。也就是相同的标签，后面的会覆盖前面的。表现就是 pom.xml优先级高于用户settings.xml高于全局settings.xml

### profile激活条件
1. 命令行 - 用户可以在 mvn 命令行中添加参数“-P”，指定要激活的 profile 的 id。如果一次要激活多个 profile，可以用逗号分开一起激活。

```shell
mvn package -P integration-tests
```

2. 默认激活

```xml
<profiles>
    <profile>
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
</profiles>
```

>[Maven 激活profile的几种方式](https://juejin.cn/post/7100837063674560549#heading-1)

## build

build 可以分为 "project build" 和 "profile build"。
```xml
  <!-- "Project Build" contains more elements than just the BaseBuild set -->
  <build>...</build>

  <profiles>
    <profile>
      <!-- "Profile Build" contains a subset of "Project Build"s elements -->
      <build>...</build>
    </profile>
  </profiles>
</project>
```

基本构建配置：

```xml
<build>
  <defaultGoal>install</defaultGoal>
  <directory>${basedir}/target</directory>
  <finalName>${artifactId}-${version}</finalName>
  <filters>
    <filter>filters/filter1.properties</filter>
  </filters>
  ...
</build>
```

defaultGoal : 默认执行目标或阶段。如果给出了一个目标，它应该被定义为它在命令行中（如 jar：jar）。如果定义了一个阶段（如安装），也是如此。

directory ：构建时的输出路径。默认为：${basedir}/target 。

finalName ：这是项目的最终构建名称（不包括文件扩展名，例如：my-project-1.0.jar）

filter ：定义 * .properties 文件，其中包含适用于接受其设置的资源的属性列表（如下所述）。换句话说，过滤器文件中定义的“name = value”对在代码中替换$ {name}字符串。 maven的默认filter文件夹为${basedir}/src/main/filters。

## rersource

```xml
        <!-- 这个元素描述了项目相关的所有资源路径列表，例如和项目相关的属性文件，这些资源被包含在
             最终的打包文件里。 --> 
        <resources> 
            <!-- 这个元素描述了项目相关或测试相关的所有资源路径 --> 
            <resource> 
                <!-- 描述了资源的目标路径。该路径相对target/classes目录（例如${project.build.outputDirectory}）。
                     举个例子，如果你想资源在特定的包里(org.apache.maven.messages)，你就必须该元素设置为
                    org/apache/maven/messages。然而，如果你只是想把资源放到源码目录结构里，就不需要该配置。 --> 
                <targetPath></targetPath> 

                <!-- 是否使用参数值代替参数名。参数值取自properties元素或者文件里配置的属性，文件在filters元素
                     里列出。 --> 
                <filtering></filtering>

                <!-- 描述存放资源的目录，该路径相对POM路径 --> 
                <directory></directory>

                <!-- 包含的模式列表，例如**/*.xml. --> 
                <includes>
                    <include></include>
                </includes>

                <!-- 排除的模式列表，例如**/*.xml -->
                <excludes>
                    <exclude></exclude>
                </excludes>
            </resource> 
        </resources> 
```

- resources: 资源元素的列表，每个资源元素描述与此项目关联的文件和何处包含文件。
- targetPath: 指定从构建中放置资源集的目录结构。目标路径默认为基本目录。将要包装在 jar 中的资源的通常指定的目标路径是 META-INF。
- filtering: 值为 true 或 false。表示是否要为此资源启用过滤。请注意，该过滤器 * .properties 文件不必定义为进行过滤 - 资源还可以使用默认情况下在 POM 中定义的属性（例如$ {project.version}），并将其传递到命令行中“-D”标志（例如，“-Dname = value”）或由 properties 元素显式定义。过滤文件覆盖上面。
- directory: 值定义了资源的路径。构建的默认目录是${basedir}/src/main/resources。
- includes: 一组文件匹配模式，指定目录中要包括的文件，使用*作为通配符。
- excludes: 与 includes 类似，指定目录中要排除的文件，使用*作为通配符。注意：如果 include 和 exclude 发生冲突，maven 会以 exclude 作为有效项。
- testResources: testResources 与 resources 功能类似，区别仅在于：testResources 指定的资源仅用于 test 阶段，并且其默认资源目录为：${basedir}/src/test/resources 。

## plugin
maven的生命周期和它所包含的若干个阶段，在每一个阶段中都会执行一些默认的操作，比如在package阶段会把compile后的.class文件打包成jar文件。在这个时候后如果想要增加一些额外的操作，比如，把项目打的jar包默认在target下，要想让它放到自己指定的某个位置。这个时候就需要用到maven提供的各种插件功能。

在maven中的插件分为两类，一类是Build plugins，在defaults生命周期里面起作用，在\<build/>配置。另外一类是Reporting plugins，在site生命周期里面起作用，在\<reporting/>配置。下面没有特别说明，都是指Build plugins。
> https://myxof.github.io/2019/01/pom.html


Maven的lifecycle，phase和goal：使用Maven构建项目就是执行lifecycle，执行到指定的phase为止。每个phase会执行自己默认的一个或多个goal。goal是最小任务单元。

如果执行：

```shell
mvn compile
```

Maven将执行compile这个phase，这个phase会调用compiler插件执行关联的compiler:compile这个goal。
实际上，执行每个phase，都是通过某个插件（plugin）来执行的，Maven本身其实并不知道如何执行compile，它只是负责找到对应的compiler插件，然后执行默认的compiler:compile这个goal来完成编译。
所以，使用Maven，实际上就是配置好需要使用的插件，然后通过phase调用它们。

如果标准插件无法满足需求，我们还可以使用**自定义插件**。使用自定义插件的时候，需要声明。例如，使用maven-shade-plugin可以创建一个可执行的jar，要使用这个插件，需要在pom.xml中声明
> https://www.liaoxuefeng.com/wiki/1252599548343744/1309301217951777

```xml
<project>
  [...]
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
        <version>3.1.1</version>
        <executions>
          <execution>
            <id>copy-jar-dependency</id>
            <phase>package</phase>
            <goals>
              <goal>copy-dependencies</goal>
            </goals>
            <configuration>
              <!-- configure the plugin here -->
              <outputDirectory>${project.basedir}/lib</outputDirectory>
            </configuration>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
  [...]
</project>
```

- groupId, artifactId, version ：和基本配置中的 groupId、artifactId、version 意义相同。
- executions - 需要记住的是，插件可能有多个目标。每个目标可能有一个单独的配置，甚至可能将插件的目标完全绑定到不同的阶段。执行配置插件的目标的执行。
  - goal 在一个maven插件里面，他有许多子功能，例如在maven-dependency-plugin里面有下面的这些功能，当你引入一个插件的时候，你需要指定自己要用到哪些子功能，也就是goal。然后在配置具体的信息。

  ```text
  dependency:analyze analyzes the dependencies of this project and determines which are: used and declared; used and undeclared; unused and declared.
  dependency:copy-dependencies takes the list of project direct dependencies and optionally transitive dependencies and copies them to a specified location, stripping the version if desired. This goal can also be run from the command line.
  ...
  dependency:unpack like copy but unpacks.
  dependency:unpack-dependencies like copy-dependencies but unpacks.
  ```

  - phase - 这个表明\<execution>里面的内容在哪个阶段会生效，\<phase>package\</phase>表明在package阶段生效，也就是说mvn package的时候这个插件会执行。如果没有配置phase，那么就会设为默认值，如默认值果为空，那么在整个生命周期里面都不会执行。

  - inherited: 像上面的继承元素一样，设置这个 false 会阻止 maven 将这个执行传递给它的子代。此元素仅对父 POM 有意义。
  - configuration: 与上述相同，但将配置限制在此特定目标列表中，而不是插件下的所有目标。


# setting.xml文件单项配置说明

## localRepository

```XML
 <!-- 本地仓库的路径。默认值为${user.home}/.m2/repository。 -->
 <localRepository>usr/local/maven</localRepository>
```

## interactiveMode

```XML
 <!--Maven是否需要和用户交互以获得输入。如果Maven需要和用户交互以获得输入，则设置成true，反之则应为false。默认为true。-->
 <interactiveMode>true</interactiveMode>
```

## usePluginRegistry

```XML
<!--Maven是否需要使用plugin-registry.xml文件来管理插件版本。如果需要让Maven使用文件${user.home}/.m2/plugin-registry.xml来管理插件版本，则设为true。默认为false。-->
 <usePluginRegistry>false</usePluginRegistry>
```

## offline

```XML
 <!--表示Maven是否需要在离线模式下运行。如果构建系统需要在离线模式下运行，则为true，默认为false。当由于网络设置原因或者安全因素，构建服务器不能连接远程仓库的时候，该配置就十分有用。 -->
 <offline>false</offline>
```

## pluginGroups

```XML
<!--当插件的组织Id（groupId）没有显式提供时，供搜寻插件组织Id（groupId）的列表。该元素包含一个pluginGroup元素列表，每个子元素包含了一个组织Id（groupId）。当我们使用某个插件，并且没有在命令行为其提供组织Id（groupId）的时候，Maven就会使用该列表。默认情况下该列表包含了org.apache.maven.plugins和org.codehaus.mojo -->
 <pluginGroups>
  <!--plugin的组织Id（groupId） -->
  <pluginGroup>org.codehaus.mojo</pluginGroup>
 </pluginGroups>
```

## proxies

```XML
<!--用来配置不同的代理，多代理profiles 可以应对笔记本或移动设备的工作环境：通过简单的设置profile id就可以很容易的更换整个代理配置。 -->
 <proxies>
  <!--代理元素包含配置代理时需要的信息-->
  <proxy>
   <!--代理的唯一定义符，用来区分不同的代理元素。-->
   <id>myproxy</id>
   <!--该代理是否是激活的那个。true则激活代理。当我们声明了一组代理，而某个时候只需要激活一个代理的时候，该元素就可以派上用处。 -->
   <active>true</active>
   <!--代理的协议。 协议://主机名:端口，分隔成离散的元素以方便配置。-->
   <protocol>http</protocol>
   <!--代理的主机名。协议://主机名:端口，分隔成离散的元素以方便配置。  -->
   <host>proxy.somewhere.com</host>
   <!--代理的端口。协议://主机名:端口，分隔成离散的元素以方便配置。 -->
   <port>8080</port>
   <!--代理的用户名，用户名和密码表示代理服务器认证的登录名和密码。 -->
   <username>proxyuser</username>
   <!--代理的密码，用户名和密码表示代理服务器认证的登录名和密码。 -->
   <password>somepassword</password>
   <!--不该被代理的主机名列表。该列表的分隔符由代理服务器指定；例子中使用了竖线分隔符，使用逗号分隔也很常见。-->
   <nonProxyHosts>*.google.com|ibiblio.org</nonProxyHosts>
  </proxy>
 </proxies>
```

## servers

```XML
<!--配置服务端的一些设置。一些设置如安全证书不应该和pom.xml一起分发。这种类型的信息应该存在于构建服务器上的settings.xml文件中。-->
 <servers>
  <!--服务器元素包含配置服务器时需要的信息 -->
  <server>
   <!--这是server的id（注意不是用户登陆的id），该id与distributionManagement中repository元素的id相匹配。-->
   <id>server001</id>
   <!--鉴权用户名。鉴权用户名和鉴权密码表示服务器认证所需要的登录名和密码。 -->
   <username>my_login</username>
   <!--鉴权密码 。鉴权用户名和鉴权密码表示服务器认证所需要的登录名和密码。密码加密功能已被添加到2.1.0 +。详情请访问密码加密页面-->
   <password>my_password</password>
   <!--鉴权时使用的私钥位置。和前两个元素类似，私钥位置和私钥密码指定了一个私钥的路径（默认是${user.home}/.ssh/id_dsa）以及如果需要的话，一个密语。将来passphrase和password元素可能会被提取到外部，但目前它们必须在settings.xml文件以纯文本的形式声明。 -->
   <privateKey>${usr.home}/.ssh/id_dsa</privateKey>
   <!--鉴权时使用的私钥密码。-->
   <passphrase>some_passphrase</passphrase>
   <!--文件被创建时的权限。如果在部署的时候会创建一个仓库文件或者目录，这时候就可以使用权限（permission）。这两个元素合法的值是一个三位数字，其对应了unix文件系统的权限，如664，或者775。 -->
   <filePermissions>664</filePermissions>
   <!--目录被创建时的权限。 -->
   <directoryPermissions>775</directoryPermissions>
  </server>
 </servers>
```

## mirrors

```XML
<!--为仓库列表配置的下载镜像列表。高级设置请参阅镜像设置页面 -->
 <mirrors>
  <!--给定仓库的下载镜像。 -->
  <mirror>
   <!--该镜像的唯一标识符。id用来区分不同的mirror元素。 -->
   <id>planetmirror.com</id>
   <!--镜像名称 -->
   <name>PlanetMirror Australia</name>
   <!--该镜像的URL。构建系统会优先考虑使用该URL，而非使用默认的服务器URL。 -->
   <url>http://downloads.planetmirror.com/pub/maven2</url>
   <!--被镜像的服务器的id。例如，如果我们要设置了一个Maven中央仓库（http://repo.maven.apache.org/maven2/）的镜像，就需要将该元素设置成central。这必须和中央仓库的id central完全一致。-->
   <mirrorOf>central</mirrorOf>
  </mirror>
 </mirrors>
```

## profiles

```XML
 <!--根据环境参数来调整构建配置的列表。settings.xml中的profile元素是pom.xml中profile元素的裁剪版本。它包含了id，activation, repositories, pluginRepositories和 properties元素。这里的profile元素只包含这五个子元素是因为这里只关心构建系统这个整体（这正是settings.xml文件的角色定位），而非单独的项目对象模型设置。如果一个settings中的profile被激活，它的值会覆盖任何其它定义在POM中或者profile.xml中的带有相同id的profile。 -->
 <profiles>
  <!--根据环境参数来调整的构件的配置-->
  <profile>
   <!--该配置的唯一标识符。 -->
   <id>test</id>
```

## Activation

```XML
<!--自动触发profile的条件逻辑。Activation是profile的开启钥匙。如POM中的profile一样，profile的力量来自于它能够在某些特定的环境中自动使用某些特定的值；这些环境通过activation元素指定。activation元素并不是激活profile的唯一方式。settings.xml文件中的activeProfile元素可以包含profile的id。profile也可以通过在命令行，使用-P标记和逗号分隔的列表来显式的激活（如，-P test）。-->
   <activation>
    <!--profile默认是否激活的标识-->
    <activeByDefault>false</activeByDefault>
    <!--当匹配的jdk被检测到，profile被激活。例如，1.4激活JDK1.4，1.4.0_2，而!1.4激活所有版本不是以1.4开头的JDK。-->
    <jdk>1.5</jdk>
    <!--当匹配的操作系统属性被检测到，profile被激活。os元素可以定义一些操作系统相关的属性。-->
    <os>
     <!--激活profile的操作系统的名字 -->
     <name>Windows XP</name>
     <!--激活profile的操作系统所属家族(如 'windows')  -->
     <family>Windows</family>
     <!--激活profile的操作系统体系结构  -->
     <arch>x86</arch>
     <!--激活profile的操作系统版本-->
     <version>5.1.2600</version>
    </os>
    <!--如果Maven检测到某一个属性（其值可以在POM中通过${name}引用），其拥有对应的name = 值，Profile就会被激活。如果值字段是空的，那么存在属性名称字段就会激活profile，否则按区分大小写方式匹配属性值字段-->
    <property>
     <!--激活profile的属性的名称-->
     <name>mavenVersion</name>
     <!--激活profile的属性的值 -->
     <value>2.0.3</value>
    </property>
    <!--提供一个文件名，通过检测该文件的存在或不存在来激活profile。missing检查文件是否存在，如果不存在则激活profile。另一方面，exists则会检查文件是否存在，如果存在则激活profile。-->
    <file>
     <!--如果指定的文件存在，则激活profile。 -->
     <exists>${basedir}/file2.properties</exists>
     <!--如果指定的文件不存在，则激活profile。-->
     <missing>${basedir}/file1.properties</missing>
    </file>
   </activation>
```

## Repositories

```XML
  <!--远程仓库列表，它是Maven用来填充构建系统本地仓库所使用的一组远程项目。 -->
   <repositories>
    <!--包含需要连接到远程仓库的信息 -->
    <repository>
     <!--远程仓库唯一标识-->
     <id>codehausSnapshots</id>
     <!--远程仓库名称 -->
     <name>Codehaus Snapshots</name>
     <!--如何处理远程仓库里发布版本的下载-->
     <releases>
      <!--true或者false表示该仓库是否为下载某种类型构件（发布版，快照版）开启。  -->
      <enabled>false</enabled>
      <!--该元素指定更新发生的频率。Maven会比较本地POM和远程POM的时间戳。这里的选项是：always（一直），daily（默认，每日），interval：X（这里X是以分钟为单位的时间间隔），或者never（从不）。 -->
      <updatePolicy>always</updatePolicy>
      <!--当Maven验证构件校验文件失败时该怎么做-ignore（忽略），fail（失败），或者warn（警告）。-->
      <checksumPolicy>warn</checksumPolicy>
     </releases>
     <!--如何处理远程仓库里快照版本的下载。有了releases和snapshots这两组配置，POM就可以在每个单独的仓库中，为每种类型的构件采取不同的策略。例如，可能有人会决定只为开发目的开启对快照版本下载的支持。参见repositories/repository/releases元素-->
     <snapshots>
      <enabled/><updatePolicy/><checksumPolicy/>
     </snapshots>
     <!--远程仓库URL，按protocol://hostname/path形式 -->
     <url>http://snapshots.maven.codehaus.org/maven2</url>
     <!--用于定位和排序构件的仓库布局类型-可以是default（默认）或者legacy（遗留）。Maven 2为其仓库提供了一个默认的布局；然而，Maven 1.x有一种不同的布局。我们可以使用该元素指定布局是default（默认）还是legacy（遗留）。 -->
     <layout>default</layout>
    </repository>
   </repositories>
   <!--发现插件的远程仓库列表。仓库是两种主要构件的家。第一种构件被用作其它构件的依赖。这是中央仓库中存储的大部分构件类型。另外一种构件类型是插件。Maven插件是一种特殊类型的构件。由于这个原因，插件仓库独立于其它仓库。pluginRepositories元素的结构和repositories元素的结构类似。每个pluginRepository元素指定一个Maven可以用来寻找新插件的远程地址。-->
   <pluginRepositories>
    <!--包含需要连接到远程插件仓库的信息.参见profiles/profile/repositories/repository元素的说明-->
          <pluginRepository>           
     <releases>      
      <enabled/><updatePolicy/><checksumPolicy/>
     </releases>
     <snapshots>
      <enabled/><updatePolicy/><checksumPolicy/>
     </snapshots>
     <id/><name/><url/><layout/>
          </pluginRepository>
        </pluginRepositories>
  </profile>
 </profiles>
```

## activeProfiles

```XML
<!--手动激活profiles的列表，按照profile被应用的顺序定义activeProfile。 该元素包含了一组activeProfile元素，每个activeProfile都含有一个profile id。任何在activeProfile中定义的profile id，不论环境设置如何，其对应的
        profile都会被激活。如果没有匹配的profile，则什么都不会发生。例如，env-test是一个activeProfile，则在pom.xml（或者profile.xml）中对应id的profile会被激活。如果运行过程中找不到这样一个profile，Maven则会像往常一样运行。 -->
   <activeProfiles>
    <activeProfile>env-test</activeProfile>
   </activeProfiles>
</settings>
```