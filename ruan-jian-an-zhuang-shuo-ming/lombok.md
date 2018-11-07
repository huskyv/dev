---
description: IEDA安装lombok插件
---

# lombok

### 介绍

#### 在项目中使用Lombok可以减少很多重复代码的书写。比如说getter/setter/toString等方法的编写。

###  IDEA中的安装

####  打开IDEA的Setting –&gt; 选择Plugins选项 –&gt; 选择Browse repositories –&gt; 搜索lombok –&gt; 点击安装 –&gt; 安装完成重启IDEA –&gt; 安装成功

![](../.gitbook/assets/image%20%284%29.png)

###  引入依赖

####  在项目中添加Lombok依赖jar，在pom文件中添加如下部分。\(不清楚版本可以在[Maven仓库](http://mvnrepository.com/)中搜索\)

```text
!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.18</version>
    <scope>provided</scope>
</dependency>
```

###  使用

 在对应的类或者方法上使用对应注解即可。例如

![](../.gitbook/assets/image%20%2814%29.png)

### Lombok常用注解

```text
@Setter
@Getter
@Data
@Log //这是一个泛型注解，具体有很多种形式
@AllArgsConstructor
@NoArgsConstructor
@EqualsAndHashCode
@NonNull
@Cleanup
@ToString
@RequiredArgsConstructor
@Value
@SneakyThrows
@Synchronized
```

