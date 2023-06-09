# SFDATA - A collection of data cleaning and handling tools by Social Finance


At Social Finance we do a lot of repetative data cleaning. Both our internal data, and that shared by clients, is often 
contained in various spreadsheets exported by a wide range of tools (or manually entered). Filenames, column names and 
column formats (such as date formats) often vary, even with the same dataset, and these often change over time meaning
cleaning has to be done again, and again... and again.

Although probably most of the datasets we process are tabular and relational in nature, this is certainly not always the case,
and in some case we need to transform from hierarchical to tabular and back. Thus this project aims to create some core
concepts that apply to both tabular and hierarchical data, as well as miscelaneous utilities for processing either.

## Similar Projects

There are many projects out there that to one degree or another deals with data binding and validation. Most (all?) [RDBMS][RDBMS] have a schema to describe the tables and relations. XML has [XML Schema][xml-schema]. There is [JSON Schema][json-schema], [CSV on the Web][tabular-data-primer], [Frictionless's Data Schema][frictionless] and many more.

This project aims to be as compatible with these as possible, whilst recognising the slightly different purpose. Whereas as most of those projects aim to be strict and limit data to those formats, this project aims to be permissive and helpful in converting incoming data to a standard form.

## Common Pipeline
At the core, we believe almost all our data pre-processing steps follow five general steps:

1. Read
2. Identify
3. Conform
4. Normalise
5. Validate

### Read

This part deals with identifying the file(s), their types and how to read them. For example a 
file can be a CSV file that needs to be turned into a singular tabular representation.

Alternatively the file may be Excel which can contain multiple tables, or even JSON with a 
hierarchical model. Locating, recognising and reading is all part of this step.

### Identify

Having now some concept of a table or record, this task aims to identify this within a pre-defined schema. That could be done by looking at the table's name (a combination of filename and other possible facets, such as sheet name in Excel or path in JSON/XML) - or it could be done by looking at the fields (columns) available in the data and match these against known types. 

The aim is for these steps to be generic enough that they can be configured for most common eventualities.

### Conform

Now that we know what we look at, this step ensures that the data representation conforms to the specification. This could involve making sure record and field/column names are set to their expected values, fixing spelling mistakes and capitalisation errors, removing whitespace and other unexpected characters etc. 

### Normalise

This step now turns the actual field values into their normal forms. For example if a value is expected to be an integer, this step ensures that the value is represented as an integer (for example "1.0" will be converted to 1), or it flags an error.

This step will also try to match categorical values to the defined set of values. 

This step is usually lenient, but should be able to be configured to either replace, retain or raise invalid values. 

### Validate

This final step can apply a set of validation rules. Simple rules include ensuring that a field is set. More complex rules could ensure that values fit within a certain range, or that one field is larger than another. 

Complex validation is currently outside the scope of this project.

## Broader Project Goals

As well as providing the pipeline, this project pulls together other useful pieces of functionality when working with data. 

The [sfdata-schema][sfdata-schema] project can also be used to generate data structure documentation and diagrams. This is particularly convenient when collaborating on a data standard. 

Wilst developing data tools, it is often good to have some sample data. The [sfdata-faker][sfdata-faker] project aims to allow the simple generation of fake data from a schema, as well as more complex generators and profiles for the sectors we do most work in, such as Children's Services.


## Sub-Projects

* [sfdata-schema][sfdata-schema] - format for describing data
* [sfdata-stream-parser][sfdata-stream-parser] - generic tools for handling incoming data
* [sfdata-pipeline][sfdata-pipeline] - standard, multi-platform, tasks for building processing pipelines
* [sfdata-faker][sfdata-faker] - providers used to generate fake data using python's faker library


[RDBMS]: https://en.wikipedia.org/wiki/Database_schema
[xml-schema]: https://www.w3.org/TR/xmlschema11-1/
[json-schema]: https://json-schema.org/
[tabular-data-primer]: https://www.w3.org/TR/tabular-data-primer/
[frictionless]: https://specs.frictionlessdata.io//table-schema/

[sfdata-schema]: https://github.com/SocialFinanceDigitalLabs/sfdata-schema
[sfdata-pipeline]: https://github.com/SocialFinanceDigitalLabs/sf-data-pipeline
[sfdata-stream-parser]: https://github.com/SocialFinanceDigitalLabs/sfdata-stream-parser
[sfdata-faker]: https://github.com/SocialFinanceDigitalLabs/sfdata-faker

