# 社区接口自动化测试

## 项目概况
+ 使用JMeter进行用例组织、编写
+ 测试用例针对应用层的接口
+ 使用ant运行用例，生成html报告
+ html报告模板基于${jmeter.home}\extras\jmeter-results-detail-report_21.xsl改写
+ 用例中的断言除了使用“响应断言”外，还通过groovy脚本实现了json断言，由此需要将下面的jar包放在${jmeterhome}/lib/ext/下

> json-unit-core-\*.jar   
> json-unit-\*.jar   
> gson-\*.jar  

## 项目目录
```
├── build.xml                             -- ant脚本
├── html-report-template.xsl              -- html报告模板
├── README.md                             -- 
├── resultLog                             -- 
│   ├── html                              -- 
│   │   └── TestReport-201707061055.html  -- html格式的报告
│   └── jtl                               -- 
│       └── TestReport-201707061055.jtl   -- jtl格式的报告（JMeter执行结果）
└── testPlan                              -- 
    ├── ****.jmx                          -- JMeter脚本
    └── ****.jmx
```

## 执行用例
+ JMeter GUI中执行单个jmx用例
+ ant批量执行所有用例 `ant -Djmeter.home="/usr/local/apache-jmeter-3.2"`，其中，jmeter.home改成本地JMeter安装路径

## 项目细节介绍
### json断言
使用了[JsonUnit](https://github.com/lukas-krecan/JsonUnit)，使用方法请自查。