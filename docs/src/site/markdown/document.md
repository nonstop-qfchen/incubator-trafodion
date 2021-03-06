<!--
  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at
 
      http://www.apache.org/licenses/LICENSE-2.0
 
  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the 
  License.
-->
This page describes how to modify the Trafodion documentation. Please refer to the [Contribute](contribute.html) page for information about other ways to contribute to the Trafodion project.

# Organization
Documents do **not** include version information as part of the file name.

## Source

Document                  | Source Format         | Source Tree                                    | Output Format
--------------------------|-----------------------|------------------------------------------------|----------------------------
Client Installation Guide | word                  | External (Word)                                | PDF
Command Interface Guide   | word                  | External (Word)                                | PDF
DCS Reference Guide       | asciidoc              | ```dcs/src/main/asciidoc```                 | Web Book, PDF
DCS APIs                  | javadoc               | ```dcs/src/main/java```                     | Web Book
odb User Guide            | word                  | External (Word)                                | PDF
REST Reference Guide      | asciidoc              | ```core/rest/src/main/asciidoc```          | Web Book, PDF
REST APIs                 | javadoc               | ```core/rest/src/main/java```               | Web Book
SQL Reference Manual      | word                  | External (Word)                                | PDF

## Web

**```docs/target/docs```** contains the **latest** version of the document. This practice makes it possible to link to a document in instructional text.

In addition, the documentation is copied to the **```docs/target/docs```** directory on a per-release basis. This directory is referred to as the **release document directory** below.

**Example**

Release Document Directory  | Content                                     | Web Site Directory
----------------------------|---------------------------------------------|----------------------------------------------------
**```docs/target/1.3.0```** | Documentation related to the 1.3.0 release. | **```incubator.trafodion.apache.org/docs/1.3.0```**
**```docs/target/1.5.0```** | Documentation related to the 1.5.0 release. | **```incubator.trafodion.apache.org/docs/1.5.0```**

The **release document directory** contains a sub-directory per document. The naming convention for these directories is the document name in all lower case without the manual/guide qualifier and with words separated by underscore. Web-based API definitions generated by **```javadoc```** are located under each sub-directory, if applicable.

**Example**

Document                  | Sub Directory Name
--------------------------|------------------------------------------
Client Installation Guide | **```client_installation```**
Command Interface Guide   | **```command_interface```**
DCS Reference Guide       | **```dcs_reference```**
odb User Guide            | **```odb_user```**
REST Reference Guide      | **```rest_reference```**
SQL Reference Manual      | **```sql_reference```**

The sub-directory is organized as follows. More files may be present in the sub-directory depending on document. 

File/Directory               | Content
-----------------------------|------------------------------------------------------------------------------------------------------
**```*.pdf```**              | The PDF version of the document. For example, **```Trafodion_SQL_Reference_Guide.pdf```**.
**```index.html```**         | Entry point for the web book. Generated by asciidoc.
**```_chapters```**          | Web book chapters; that is, the actual content.
**```apidocs```**            | API documentation provided as web. Generated by javadoc.
**```apidocs/index.html```** | Entry point for API documentation.
**```css```**                | CSS definitions used by the web-version of the document.
**```images```**             | Images used by the web-version of the document.

# Making Changes

## Word Documents
Do the following:

1. Edit the document.
2. Save a PDF version.
3. Build the web site using **```mvn clean site```** against the **```docs```** directory.
4. Create the **Release Document Directory**, if needed.
5. Copy the PDF files to the **Release Document Directory**.
6. Copy and overwrite the PDF to the **```docs/target/docs```** directory — latest version of the document.

## Asciidoc Documents
Please refer to DCS [Contributing to Documentation](https://github.com/apache/incubator-trafodion/blob/master/dcs/src/main/asciidoc/_chapters/appendix_contributing_to_documentation.adoc) guidance for information about working on asciidoc-based documentation.

Once you've made the desired changes, then do the following:

1. Build the document using **```mvn clean site```** against the directory containing the document; for example: **```dcs```** or **```core/rest'''**.
2. Verify the content in the generated **```target```** directory. The **```target/index.html```** file provides the entry point for the web book; the **```target/apidocs/index.html```** file contains the entry point for API documentation.

You will need to move the files to the final **Release Document Directory**; refer to [Publishing](#Publishing) below.

# Publishing

<div class="alert alert-dismissible alert-info">
  <button type="button" class="close" data-dismiss="alert">&close;</button>
  <p style="color:black">Publication is done when a committer is ready to update the external web site. You do <strong>not</strong> perform these steps as part of checking in changes.</p></div>

**Prerequisite:** You need to build the web site before using these instructions. Please refer to [Modifying Web Site](website.html).

You will need to copy/move the documentation from its generated location to the **Release Document Directory**.

1. Create the **Release Document Directory** under **```docs/target/docs```** if it doesn't already exist.
2. Copy the generated document files as follows:

Document                  | Populate Release Document Directory
--------------------------|------------------------------------------
Client Installation Guide | Copy the **```.pdf```** file to **```docs/target/docs```** and **Release Document Directory**.
Command Interface Guide   | Copy the **```.pdf```** file to **```docs/target/docs```** and **Release Document Directory**.
DCS Reference Guide       | Copy **```dcs/target/site/```** to the **Release Document Directory**.
odb User Guide            | Copy the **```.pdf```** file to **```docs/target/docs```** and **Release Document Directory**.
REST Reference Guide      | Copy **```core/rest/target/site/```** to the **Release Document Directory**.
SQL Reference Manual      | Copy the **```.pdf```** file to **```docs/target/docs```** and **Release Document Directory**.

**Example — Publishing the DCS Reference Guide**

    cd $SQ_HOME/docs/target/docs
    mkdir 1.3.0
    cd 1.3.0
    mkdir dcs_reference
    cp -r $SQ_HOME/dcs/target/site/ .

Once the update of the **Release Document Directory** is complete, then you can complete the [web-site publication](website.html#Publishing).

