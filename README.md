# mybatis-generator-pager-plugin
A MyBatis Generator plugin for MySQL pagination use limit.

## MySQL Usage

在MyBatis Generator configuration file增加插件配置
  `<plugin type="com.yulongs.mybatis.plugins.MySQLPaginationPlugin"></plugin>` 

```
<generatorConfiguration>
    <context id="mysqlgenerator" targetRuntime="MyBatis3">
    	<plugin type="com.yulongs.mybatis.plugins.MySQLPaginationPlugin"></plugin>
    	...
    </context>
</generatorConfiguration>
```

### Running with Maven

pom.xml

```
<pluginRepositories>
	<pluginRepository>
		<id>mybatis-generator-limit-plugin-mvn-repo</id>
		<url>https://raw.github.com/xxx</url>
	</pluginRepository>
</pluginRepositories>
```

```
<build>
	<plugins>
		<plugin>
			<groupId>org.mybatis.generator</groupId>
			<artifactId>mybatis-generator-maven-plugin</artifactId>
			<version>1.3.2</version>
			<dependencies>
				<dependency>
					<groupId>mysql</groupId>
					<artifactId>mysql-connector-java</artifactId>
					<version>5.1.34</version>
				</dependency>
				<dependency>
					<groupId>com.yulongs</groupId>
					<artifactId>mybatis-generator-plugin</artifactId>
					<version>1.0.0</version>
				</dependency>
			</dependencies>
			<configuration>
				<overwrite>true</overwrite>
			</configuration>
		</plugin>
	</plugins>
</build>
```

Run `mvn mybatis-generator:generator` to generate java and xml files.

### Using the Generated Objects

```
XxxExample example = new XxxExample();
...
example.setLimit(10); // page size limit
example.setOffset(20); // offset
List<Xxx> list = xxxMapper.selectByExample(example);
```
The SQL will be:
`select ... limit 20, 10`

```
XxxExample example = new XxxExample();
...
example.setLimit(10); // limit
List<Xxx> list = xxxMapper.selectByExample(example);
```
The SQL will be:
`select ... limit 10`

### Download
Jar: 
