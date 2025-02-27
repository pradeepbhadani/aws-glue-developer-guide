# Working with Classifiers on the AWS Glue Console<a name="console-classifiers"></a>

A classifier determines the schema of your data\. You can write a custom classifier and point to it from AWS Glue\. 

## Viewing Classifiers<a name="view-classifiers-console"></a>

To see a list of all the classifiers that you have created, open the AWS Glue console at [https://console\.aws\.amazon\.com/glue/](https://console.aws.amazon.com/glue/), and choose the **Classifiers** tab\.

The list displays the following properties about each classifier:
+ **Classifier** – The classifier name\. When you create a classifier, you must provide a name for it\.
+ **Classification** – The classification type of tables inferred by this classifier\.
+ **Last updated** – The last time this classifier was updated\.

## Managing Classifiers<a name="manage-classifiers-console"></a>

From the **Classifiers** list in the AWS Glue console, you can add, edit, and delete classifiers\. To see more details for a classifier, choose the classifier name in the list\. Details include the information you defined when you created the classifier\.  

## Creating Classifiers<a name="add-classifier-console"></a>

To add a classifier in the AWS Glue console, choose **Add classifier**\. When you define a classifier, you supply values for the following:
+ **Classifier name** – Provide a unique name for your classifier\.
+ **Classifier type** – The classification type of tables inferred by this classifier\.
+ **Last updated** – The last time this classifier was updated\.

**Classifier name**  
Provide a unique name for your classifier\.

**Classifier type**  
Choose the type of classifier to create\.

Depending on the type of classifier you choose, configure the following properties for your classifier:

------
#### [ Grok ]
+ **Classification** 

  Describe the format or type of data that is classified or provide a custom label\. 
+ **Grok pattern** 

  This is used to parse your data into a structured schema\. The grok pattern is composed of named patterns that describe the format of your data store\. You write this grok pattern using the named built\-in patterns provided by AWS Glue and custom patterns you write and include in the **Custom patterns** field\. Although grok debugger results might not match the results from AWS Glue exactly, we suggest that you try your pattern using some sample data with a grok debugger\. You can find grok debuggers on the web\. The named built\-in patterns provided by AWS Glue are generally compatible with grok patterns that are available on the web\. 

  Build your grok pattern by iteratively adding named patterns and check your results in a debugger\. This activity gives you confidence that when the AWS Glue crawler runs your grok pattern, your data can be parsed\.
+ **Custom patterns** 

  For grok classifiers, these are optional building blocks for the **Grok pattern** that you write\. When built\-in patterns cannot parse your data, you might need to write a custom pattern\. These custom patterns are defined in this field and referenced in the **Grok pattern** field\. Each custom pattern is defined on a separate line\. Just like the built\-in patterns, it consists of a named pattern definition that uses [regular expression \(regex\)](http://en.wikipedia.org/wiki/Regular_expression) syntax\. 

  For example, the following has the name `MESSAGEPREFIX` followed by a regular expression definition to apply to your data to determine whether it follows the pattern\. 

  ```
  MESSAGEPREFIX .*-.*-.*-.*-.*
  ```

------
#### [ XML ]
+ **Row tag** 

  For XML classifiers, this is the name of the XML tag that defines a table row in the XML document\. Type the name without angle brackets `< >`\. The name must comply with XML rules for a tag\.

  For more information, see [Writing XML Custom Classifiers](custom-classifier.md#custom-classifier-xml)\. 

------
#### [ JSON ]
+ **JSON path** 

  For JSON classifiers, this is the JSON path to the object, array, or value that defines a row of the table being created\. Type the name in either dot or bracket JSON syntax using AWS Glue supported operators\. 

  For more information, see the list of operators in [Writing JSON Custom Classifiers](custom-classifier.md#custom-classifier-json)\. 

------
#### [ CSV ]
+ **Column delimiter** 

  A single character or symbol to denote what separates each column entry in the row\. Choose the delimiter from the list, or choose `Other` to enter a custom delimiter\.
+ **Quote symbol** 

  A single character or symbol to denote what combines content into a single column value\. Must be different from the column delimiter\. Choose the quote symbol from the list, or choose `Other` to enter a custom quote character\.
+ **Column headings** 

  Indicates the behavior for how column headings should be detected in the CSV file\. You can choose `Has headings`, `No headings`, or `Detect headings`\. If your custom CSV file has column headings, enter a comma\-delimited list of the column headings\. 
+ **Allow files with single column** 

  To be classified as CSV, the data must have at least two columns and two rows of data\. Use this option to allow the processing of files that contain only one column\.
+ **Trim whitespace before identifying column values** 

  This option specifies whether to trim values before identifying the type of column values\.

------

For more information, see [Writing Custom Classifiers](custom-classifier.md)\.