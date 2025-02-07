Keep it stupid and simple, try direct/absolute path
Traversal may be stripped  `../` , can use  `....//` to have inner part removed and then the resulting string would be a traversal string
Single or double URL encoding  `../../../../etc/passwd` to `%252E%252E%252F%252E%252E%252F%252E%252E%252F%252E%252E%252Fetc%252Fpasswd`
Use null-bytes for extensions on files `filename=../../../etc/passwd%00.png`

Below is an example of some simple Java code to validate the canonical path of a file based on user input:

```java
File file = new File(BASE_DIRECTORY, userInput); 
if (file.getCanonicalPath().startsWith(BASE_DIRECTORY)) { 
// process file 
}
```