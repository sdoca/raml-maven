# RAML Maven Plugin
[![Build Status](https://travis-ci.org/CJSCommonPlatform/raml-maven.svg?branch=master)](https://travis-ci.org/CJSCommonPlatform/raml-maven) 
[![Coverage Status](https://coveralls.io/repos/github/CJSCommonPlatform/raml-maven/badge.svg?branch=master)](https://coveralls.io/github/CJSCommonPlatform/raml-maven?branch=master)

This project contains a plugin for using [RAML](http://raml.org/) documents within Maven projects.
Currently, it has two purposes:

- _Code generation_ - the plugin can be configured with arbitrary code generation modules to generate custom code from RAML documents
- _RAML syntax checking_ - for validating the syntax of RAML documents and imported JSON schemas

## Usage

For example, to generate code using a generator class `ExampleGenerator` using RAML from an external
Maven dependency:

```xml
<build>
    <plugins>
        <plugin>
            <artifactId>raml-maven-plugin</artifactId>
            <groupId>uk.gov.justice.maven</groupId>
            <version>1.1.1</version>
            <executions>
                <execution>
                    <configuration>
                        <generatorName>
                            uk.gov.justice.raml.maven.test.ExampleGenerator
                        </generatorName>
                        <basePackageName>uk.gov.justice.api</basePackageName>
                        <outputDirectory>${project.build.directory}/generated-sources</outputDirectory>
                        <sourceDirectory>CLASSPATH</sourceDirectory>
                        <includes>
                            <include>**/*external-*.raml</include>
                        </includes>
                        <excludes>
                            <exclude>**/*external-ignore.raml</exclude>
                        </excludes>
                    </configuration>
                    <goals>
                        <goal>generate</goal>
                    </goals>
                    <phase>generate-sources</phase>
                </execution>
            </executions>
            <dependencies>
                <dependency>
                    <groupId>uk.gov.justice.maven</groupId>
                    <artifactId>raml-for-testing-io</artifactId>
                    <version>${project.version}</version>
                    <classifier>raml</classifier>
                </dependency>
            </dependencies>
        </plugin>
    </plugins>
</build>
```
