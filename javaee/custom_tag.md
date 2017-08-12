# Chapter 6 JSP custom tag

> A custom tag is a user-defined JSP language element
> When a JSP page containing a custom tag is translated into a servlet, the tag is converted to operations on an object called a tag handler.
> The Web container then invokes those operations when the JSP page's servlet is executed.

1.  extends `javax.servlet.jsp.tagext.SimpleTagSupport` class
2.  override `doTag()` method

	```java
	package demo;
	
	import javax.servlet.jsp.JspException;
	import javax.servlet.jsp.JspWriter;
	import javax.servlet.jsp.tagext.SimpleTagSupport;
	import java.io.IOException;
	
	public class TestTag extends SimpleTagSupport {
	    @Override
	    public void doTag() throws JspException, IOException {
	        JspWriter jspWriter = getJspContext().getOut();
	        jspWriter.print("test...");
	    }
	}
	```

3. create `WEB-INF/test.tld`

	```xml
	<taglib>
	    <tlib-version>1.0</tlib-version>
	    <jsp-version>2.0</jsp-version>
	    <short-name>Test TLD</short-name>
	    <tag>
	        <name>Test</name>
	        <tag-class>demo.TestTag</tag-class>
	        <body-content>empty</body-content>
	    </tag>
	</taglib>
	```

4. create `test.jsp`	

	```html
	<%@ page contentType="text/html;charset=UTF-8" language="java" %>
	<%@ taglib prefix="t" uri="/WEB-INF/test.tld" %>
	<html>
	<head>
	    <title>Test Tag</title>
	</head>
	<body>
	<t:Test/>
	</body>
	</html>
	```
5. Attributes

	- Edit Tag class
	
		```java
		// ...
		private String attr;
		
		public void setAttr(String attr) {
			this.attr = attr;
		}
		// ...
		```
	- Edit TLD file

		```xml
		<!-- ... -->
		<body-content>scriptless</body-content>
		<attribute>
		    <name>attr</name>
		    <required>true</required>
		    <type>java.lang.String</type>
		</attribute>
		<!-- ... -->
		```
	- Edit JSP file
	
		```html
		<t:Test attr="some attr...">
		```
		