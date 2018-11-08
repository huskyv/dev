# Maven私服配置

### 打包到私服\(pom.xml\)

```text
<!-- 项目部署到私服配置 -->  
<distributionManagement> <!-- 远程部署管理信息 -->  
    <repository> <!--部署项目产生的构件到远程仓库需要的信息 -->  
        <id>releases</id>  
        <name>Nexus Release Repository</name>  
    <url>http://127.0.0.1:8081/nexus/content/repositories/releases/</url>  
    </repository>  
    
    <snapshotRepository> <!-- 如果没有配置该元素，默认部署到repository元素配置的仓库 -->  
        <id>snapshots</id>  
        <name>Nexus Snapshot Repository</name>  
        <url>http://127.0.0.1:8081/nexus/content/repositories/snapshots/</url>  
    </snapshotRepository>  
</distributionManagement>  
```

### 指定maven地址下载jar包到本地\(pom.xml\)

```text
<repository>
       <id>jeecg</id>
       <name>jeecg Repository</name>
       <url>http://maven.jeecg.org/nexus/content/repositories/jeecg</url>
       <snapshots>
    <enabled>false</enabled>
</repository>
```

### 私服用户名密码配置（setting.xml ）

```text
<server>
    <id>nexus-releases</id>
    <username>admin</username>
    <password>admin123</password>
 </server>
        
 <server>
    <id>nexus-snapshots</id>
    <username>admin</username>
    <password>admin123</password>
 </server>
```

