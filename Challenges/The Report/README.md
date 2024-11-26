# The Report
## Challenge Brief

> ![image](https://github.com/user-attachments/assets/e6b9799a-92aa-4df2-b2ec-19f74aa9decb)

## Scenario
> You are working in a newly established SOC where still there is lot of work to do to make it a fully functional one. As part of gathering intel you were assigned a task to study a threat report released in 2022 and suggest some useful outcomes for your SOC.

## Setup
1. Download the file and unzip the file.
2. Readed the extracted PDF file.
   
## Question 1) Name the supply chain attack related to Java logging library in the end of 2021 (Format: AttackNickname) 
qqqq
qqqq

---

## Question 2) Mention the MITRE Technique ID which effected more than 50% of the customers (Format: TXXXX) 

1. Go to VirusTotal, upload the *sample.doc* file, and analyse the generated report. The full filetype of the provided sample is **Office Open XML Document**.

   ![image](https://github.com/ZuanAce/blueteamlabs/assets/147037911/b5de49bd-76f4-4f26-ae2e-1a835822a223)

# Question 3) Extract the URL that is used within the sample and submit it (Format: https://x.domain.tld/path/to/something)
1. To analyse the file, extract the content of the DOC file by running the command *unzip sample.doc*.
2. Using the command *cat word/_rels/document.xml.rels* to examine the content of the "word/_rels/document.xml.rels" file. This file seems suspicious because it stands for "Relationships part" and plays a crucial role in defining relationships between various parts of the document.
   
   ![image](https://github.com/ZuanAce/blueteamlabs/assets/147037911/f230bbd4-f560-4397-9915-5ea993883bed)
   
3. The output displays the following findings:
   ```
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <Relationships xmlns="http://schemas.openxmlformats.org/package/2006/relationships">
   <Relationship Id="rId3" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/webSettings" Target="webSettings.xml"/>
   <Relationship Id="rId2" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/settings" Target="settings.xml"/><Relationship Id="rId1"
   Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles" Target="styles.xml"/><Relationship Id="rId996"
   Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/oleObject" Target="https://www.xmlformats.com/office/word/2022/wordprocessingDrawing/RDF842l.html!" TargetMode="External"/
   <Relationship Id="rId5" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/theme" Target="theme/theme1.xml"/><Relationship Id="rId4"
   Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/fontTable" Target="fontTable.xml"/></Relationships>  
   ```
4. In the XML snippet, there's a line that specifies a link to an external web page. This line has an ID, a type indicating it's related to an embedded object, and a URL (web address) pointing to the specific page. The URL, https://www.xmlformats.com/office/word/2022/wordprocessingDrawing/RDF842l.html, is where the document is trying to connect to. It's like a shortcut within the document that leads to content on the internet.


# Question 4) What is the name of the XML file that is storing the extracted URL? (Format: file.name.ext)
1. Refer to Question 3, the file name is **document.xml.rels**.

# Question 5) The extracted URL accesses a HTML file that triggers the vulnerability to execute a malicious payload. According to the HTML processing functions, any files with fewer than <Number> bytes would not invoke the payload. Submit the <Number> (Format: Number of Bytes) 
1. Based on the Huntress report, any files with fewer than 4096 bytes would not invoke the payload.
   
   ![image](https://github.com/ZuanAce/blueteamlabs/assets/147037911/bff4caad-e572-4932-8474-eafc90759c5e)

# Question 6) After execution, the sample will try to kill a process if it is already running. What is the name of this process? (Format: filename.ext) 
1. Examining the Huntress report reveals the sequence of events when the malware is executed, providing insights into the exploit's behavior. This information addresses the sixth question in the analysis.
   
   ![image](https://github.com/ZuanAce/blueteamlabs/assets/147037911/03a6cb19-2930-407d-833d-29d0eefa0578)

# Question 7) You were asked to write a process-based detection rule using Windows Event ID 4688. What would be the ProcessName and ParentProcessname used in this detection rule? [Hint: OSINT time!] (Format: ProcessName, ParentProcessName)
1. In the report, there's a picture showing how one computer process leads to another. We can create a way to detect this because the way these processes are connected looks strange. This helps us answer question 7 in the investigation.
   
   ![image](https://github.com/ZuanAce/blueteamlabs/assets/147037911/2be1d883-2244-4d36-88fd-f70901cfc5f1)

# Question 8) Submit the MITRE technique ID used by the sample for Execution [Hint: Online sandbox platforms can help!] (Format: TXXXX) 
1. Head over to VirusTotal and click on the Behavior tab. Scroll down, and you'll find the MITRE technique ID that the sample uses for its Execution behavior.
   
   ![image](https://github.com/ZuanAce/blueteamlabs/assets/147037911/526293a7-268b-48a5-b52d-bff24e8cb43b)

# Question 9) Submit the CVE associated with the vulnerability that is being exploited (Format: CVE-XXXX-XXXXX)
1. Check the Detection tab. The CVE associated **cve-2022-30190**.
   
   ![image](https://github.com/ZuanAce/blueteamlabs/assets/147037911/286cfe58-1288-4fa8-8cc0-303f7bb7b108)
