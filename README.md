# Customized-Print-Solution-ServiceNow
Objective: To create a Custom PDF of any record/form/page in ServiceNow. We have used MidServer to create the PDF and attach back to the record. Currently we have the facility to create a standard Pdf from the record. But this solution could be used to create any kind of custom Pdf and populate values from the record.

Key points: 
Was able to get the header and footer in each PDF page just with html and style sheet

Documentation For Print Functionality

1.	Setting up Mid Server

2.	External Libraries Setup 

3.	Script Include to Probe the MidServer and generate the byte stream

4.	Creation of UI action button 

5.	Creation of Custom UI page which matches the PDF

6.	Sending the PDF back as Payload and attach it to the ECC queue using Business Rule – Attachment Creator

Detailed Steps
1. Please follow the MID server set up documentation for setting up either Windows or Linux Mid Server
2.  Flying Saucer – Google project open source – and it is uses the older version of iText which finally helped me create PDF and also allowed us to use CSS 3 which makes it easier in terms of adding header and footer using styles rather than code which makes it more maintainable. 
https://code.google.com/archive/p/flying-saucer

Also add the following jar files with the flying saucer project. To add these jar files go to JAR files under MidServer, unzip the main file obtained from the below repository and add the below mentioned jar file the unzipped folder.

a.	core-renderer
b.	iText
c.	xml-apis-xerces

Kindly restart your mid server once the JAR file have been installed. 

3. Once the Mid server and the external libraries have been installed, GenerateAndAttachPdf   Script Include needs to be added to the script include in MidServer. There is a separate file in the main trunk with comments in it. This script includes processes the html response it receives, cleans it, converts it to PDF and sends it back to ServiceNow.

4. Next is the creation of business rule on ECC queue table with condition current.topic ==”AttachmentCreator” 

The code for the business rule is checked into trunk as AttachmentCreator.

5. Once you create the business rule, you can create the UI action to generate the PDF out of any form.
The sample code to do that is enlisted under the file UIButtonAction.

6. Lastly you would need to create a UI page, which maps to your custom PDF.  I have created a sample UI page, which shows you main elements. And for convenience I have added the header and footer piece that repeats on each PDF. 


