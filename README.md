# Grails Plugin Build

## Create new Grails Plugin

```dotnetcli
sdk use grails 5.1.7
grails create-plugin org.grails.demos.grails-plugin-depend-on-issue
```

## Package the Grails Plugin

I update the `GrailsPluginDependOnIssueGrailsPlugin.groovy`, add two properties: `version` and `dependsOn`.

`src/main/groovy/org/grails/demos/GrailsPluginDependOnIssueGrailsPlugin.groovy`

```groovy

class GrailsPluginDependOnIssueGrailsPlugin extends Plugin {

    def version = GrailsUtil.getGrailsVersion()
    def dependsOn = [core: version, domainClass: version, services: version]

}
```

Then I run this command to package the plugin, this task also generate `grails-plugin.xml` for it, but the `version` and `dependsOn` nodes were not right as expected.

```
./gradlew build
```

`build/classes/groovy/main/META-INF/grails-plugin.xml`

```xml
<plugin name='grailsPluginDependOnIssue' version='0.1' grailsVersion='5.1.7 &gt; *'>
  <type>org.grails.demos.GrailsPluginDependOnIssueGrailsPlugin</type>
  <grailsVersion>5.1.7 &gt; *</grailsVersion>
  <authorEmail></authorEmail>
  <pluginExcludes>[grails-app/views/error.gsp]</pluginExcludes>
  <dependsOn core='version' domainClass='version' services='version' />
  <author>Your name</author>
  <documentation>http://grails.org/plugin/grails-plugin-depend-on-issue</documentation>
  <profiles>[web]</profiles>
  <name>grails-plugin-depend-on-issue</name>
  <description>Brief summary/description of the plugin.
</description>
  <title>Grails Plugin Depend On Issue</title>
  <version />
  <resources>
    <resource>org.grails.demos.UrlMappings</resource>
    <resource>org.grails.demos.Application</resource>
    <resource>org.grails.demos.BootStrap</resource>
  </resources>
</plugin>
```

