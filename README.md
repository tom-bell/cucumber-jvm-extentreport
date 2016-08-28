# cucumber-jvm-extentreport [![Build Status](https://travis-ci.org/haroon-sheikh/cucumber-jvm-extentreport.svg?branch=master)](https://travis-ci.org/haroon-sheikh/cucumber-jvm-extentreport)

A custom `cucumber-jvm` report formatter using [ExtentReports](http://extentreports.relevantcodes.com)

## Usage
Add the following to your list of dependencies in `pom.xml`

```
<dependency>
    <groupId>com.sitture</groupId>
    <artifactId>cucumber-jvm-extentsreport</artifactId>
    <version>1.0.0</version>
</dependency>
```

## Cucumber Runner
Add the following to your cucumber runner class:

```java
@RunWith(Cucumber.class)
@CucumberOptions(plugin = {"com.sitture.ExtentFormatter"})
public class RunCukesTest {
    @BeforeClass
    public static void setup() {
        // Initiates the extent report and generates the output in the target/extent-report/<TIMESTAMP>/index.html file by default.
        ExtentFormatter.initiateExtentFormatter();

        // Loads the extent config xml to customize on the report.
        ExtentFormatter.loadConfig(new File("src/test/resources/config.xml"));

        ExtentFormatter.addSystemInfo("Browser", "Chrome");
		ExtentFormatter.addSystemInfo("Selenium", "v2.53.1");

		Map<String, String> systemInfo = new HashMap<String, String>();
		systemInfo.put("Cucumber", "v1.2.4");
		systemInfo.put("Extent Reports", "v2.41.1");
		ExtentFormatter.addSystemInfo(systemInfo);
    }
}
```
### Reports Location

By default, reports are generated at `targer/extent-report/<TIMESTAMP>/index.html`. To change the default location, add a parameter when initializing the report. E.g.

```java
ExtentFormatter.initiateExtentFormatter(new File(target/myNewLocation/index.html));
```

### Configuration file

Refer here to create the config xml file: [ExtentReports Configuration](http://extentreports.relevantcodes.com/java/#configuration)
To load the config file:

```
ExtentFormatter.loadConfig(new File("your config xml file path"));
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request