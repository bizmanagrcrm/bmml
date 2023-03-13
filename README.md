# bmml
A markdown language for BizmanageCRM


## Introduction

At BizmanageCRM we allow you to write custom code that will be embeded in the system. 



## Syntax

Almost any HTML document (that is valid HTML) is a valid bmml document. The only exception are elements that belong outside of the `<body>` section. These tags are managed automatically by the system and should not be included in the custom page;


## BMML Elements


### `<bmml-report>`
This element is used to embed a report in the page. The report is identified by its id.
example:
```<bmml-report id="1"></bmml-report>```

