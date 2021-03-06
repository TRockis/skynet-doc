# 3.1.1 服务开发

开发步骤

1. 引入 Skynet起步依赖
2. 实现插件接口
3. 插件Action配置
4. 编译打包
5. 部署测试

## Skynet起步依赖

目前skynet所依赖的包全部放在Maven仓库上面，配置仓库地址，则可以获得skynet全部依赖。

> pom.xml maven 依赖

```markup
<parent>
    <groupId>com.iflytek.skynet</groupId>
    <artifactId>skynet-cloud-starter-parent</artifactId>
    <version>{版本号}</version>
</parent>

<properties>
    <mvn-repo>http://pl.maven.iflytek.com/nexus</mvn-repo>
</properties>

<repositories>
    <repository>
        <id>repo1-cache</id>
        <name>repo1-cache</name>
        <url>${mvn-repo}/content/groups/public</url>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
    </repository>
    <repository>
        <id>repo2-cache</id>
        <name>repo2-cache</name>
        <url>${mvn-repo}/content/repositories/skynet-releases</url>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
    </repository>
    <repository>
        <id>repo3-cache</id>
        <name>repo3-cache</name>
        <url>${mvn-repo}/content/repositories/skynet-snapshots</url>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
    </repository>
</repositories>
```

## 实现插件接口

以Web服务为例，需要实现RestSvcContext接口，下面是接口定义

```java
public interface RestSvcContext extends AutoCloseable {

    /**
     * 服务 名称
     */
    String getSvcName();

    /**
     * 初始化
     */
    void init(AppContext appContext, Map<String, Object> params) throws Exception;

    /**
     * 服务状态
     */
    Map<String, Object> getState() throws Exception;
}
```

实现类示例

```java
@AntAction(name = RestSvc.SvcName, type = AntActionType.rest)
@Component(RestSvc.SvcName)
public class RestSvc implements RestSvcContext {

    public static final String SvcName = "sample.rest.app";

    @Override
    public String getSvcName() {
        return null;
    }

    @Override
    public void init(AppContext appContext, Map<String, Object> params) throws Exception {
        // 开始进行引擎初始化
    }

    @Override
    public Map<String, Object> getState() {
        return null;
    }

    @Override
    public void close() throws Exception {

    }
}
```

## Action配置

