# refaster

Refaster Rules - Maven

## How to Use

Edit the rules and compile through Maven:

```
mvn clean compile
```

Copy the file `rules.refaster` to the desired repo, and use it in the target repository as a plugin:

```
	<plugin>
		<groupId>org.apache.maven.plugins</groupId>
		<artifactId>maven-compiler-plugin</artifactId>
		<version>3.8.1</version>
		<configuration>
			<release>${java.version}</release>
			<source>${maven.compiler.source}</source>
			<target>${maven.compiler.target}</target>
			<testSource>${maven.compiler.source}</testSource>
			<testTarget>${maven.compiler.target}</testTarget>
			<encoding>${project.build.sourceEncoding}</encoding>
			<compilerArgs>
				<arg>-XDcompilePolicy=simple</arg>
				<arg>-Xplugin:ErrorProne -XepPatchChecks:refaster:${maven.multiModuleProjectDirectory}\rules.refaster -XepPatchLocation:IN_PLACE</arg>
			</compilerArgs>
			<annotationProcessorPaths>
				<path>
					<groupId>com.google.errorprone</groupId>
					<artifactId>error_prone_refaster</artifactId>
					<version>2.4.0</version>
				</path>
			</annotationProcessorPaths>
		</configuration>
	</plugin>
```