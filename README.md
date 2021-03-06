[简体中文](./README.cn.md) | English

[TOC]

The purpose of this project is to help you automate Web API testing, such as HTTP interface. It uses JMeter to record, edit, organize test cases. Use Ant to execute cases in batch and output result report in HTML format. Moreover, it can be used in combination with Jenkins.


# Project Brief

+ Use JMeter to record http request, write test cases, organize cases and check results(assert).
+ Use Ant to run cases in batch, and then generate html report
+ html report is customized based on the template `${jmeter.home}\extras\jmeter-results-detail-report_21.xsl`
+ In test cases, besides of response assertion built-in, I add `JSON Schema assertion` to validate the JSON Schema of response. To use JSON Schema assertion, you have to place following jars into `${jmeterhome}/lib/ext/`. Search and download the jars on: [https://www.mvnrepository.com](https://www.mvnrepository.com)
    > json-unit-core-\*.jar  
    > json-unit-\*.jar  
    > gson-\*.jar


# Project Structure

```
├── build.xml                             -- Ant script
├── html-report-template.xsl              -- html template
├── README.md
├── resultLog                             -- running log
│   ├── html
│   │   └── TestReport-201707061055.html  -- report in html format
│   └── jtl
│       └── TestReport-201707061055.jtl   -- report in jtl format, the default of JMeter
└── testPlan                              -- test case suite
    ├── expectjson                        -- expected value in JSON format
    │   └── ****.json
    ├── ****.jmx                          -- JMeter script
    └── ****.jmx
```


# Run test cast

![JMeter main GUI](/doc/JMeter-main-GUI.png)

+ Method 1: Run a single JMX test case in the JMeter GUI
+ Method 2: Use Ant to run all cases in batch. In the project root directory, run the command `ant -Djmeter.home="/usr/local/apache-jmeter-3.2"`, note that change the value of jmeter.home to your local install path of JMeter


# Project details

## the examples
1. `example_login-with-cookie.jmx` demonstrates the contents:
    + set the parameters which are used in request, assertion
    + extract parameters from http response
    + pass parameters from one request to another
    + how to write response assertion
    + how to write JSON assertion, **putting the stuff `expectjson={demo.json}` in `comment` of request**
    + how to set http proxy recorder

2. `example_login-with-token.jmx` demonstrates the contents:
    + extract token from Response in API
    + use the above token in the Header of subsequent Resquest

## JSON Schema assertion

`JSON Schema assertion` is used to verify the JSON Schema, rather than to check the values in JSON. This is the difference between `JSON assertion` which is built-in by JMeter.

`JSON Schema assertion` is written in Groovy language. 

![JSON Schema Assertion](/doc/JSON-Schema-Assertion.png)

Based on [JsonUnit](https://github.com/lukas-krecan/JsonUnit), there are lots of useful tools in it. See the website for more information.
