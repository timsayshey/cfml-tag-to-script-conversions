# CFML Tag to Script Conversions
#####A collection of examples demonstrating the conversion of CFML code blocks written in tags to CFScript.

**Currently a work in progress!**

> This is not the CFScript syntax documentation you're (possibly) looking for. That awesome piece of work, by Adam Cameron, can be found [here](https://github.com/adamcameron/cfscript) and is highly recommended as a reference to the content you'll find here.

> If you happen to be searching for a resource to learn CFML, check out [CFML in 100 Minutes](https://github.com/mhenke/CFML-in-100-minutes/wiki) by Mike Henke & [Learn CF in a Week](http://www.learncfinaweek.com/) by [this solid bunch of devs](http://www.learncfinaweek.com/contributors/).

The examples in this document are an attempt to demonstrate conversions of CFML tag-based code to script-based code as a way of learning / migrating to CFScript. It is assumed that you already have a relatively firm understanding of the ColdFusion Markup Language (at least on a tag-based level). For the sake of modernity, the converted examples will be written to comply (from an agnostic approach) with the most current versions of the various CFML engines at the time of writing - (ColdFusion 11, Railo 4.2 & Lucee 4.5).

## Table of Contents
1. [The Modern Implementation of Tags to Script](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#the-modern-implementation-of-tags-to-script)
2. [Comments](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#comments)
3.  [Variables](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#variables)
4. [Operators](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#operators)
 - [Decision](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#decision)
 - [Increment / Decrement](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#increment--decrement)
 - [Inline Assignment](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#inline-assignment)
 - [Boolean](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#boolean)
 - [Ternary & Null-Coalescing](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#ternary--null-coalescing)
5. [Conditions](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#conditions)
 - [cfif / cfelseif / cfelse](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfif--cfelseif--cfelse)
 - [cfswitch](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfswitch)
 - [cftry / cfcatch / cffinally](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cftry--cfcatch--cffinally)
 - [cfthrow & cfrethrow](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfthrow--cfrethrow)
6. [Iterations](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#iterations)
 - [General Purpose Loop](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#general-purpose-loop)
 - [Array Loop](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#array-loop)
 - [Struct Loop](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#struct-loop)
 - [List Loop](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#list-loop)
 - [Query Loop](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#query-loop)
7. [Other Flow Control Tags](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#other-flow-control-tags)
 - [cfabort & cfexit](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfabort--cfexit)
8. [General](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#general)
 - [cfoutput](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfoutput)
 - [cfsavecontent](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfsavecontent)
 - [cfthread](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfthread)
 - [cflock](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cflock)
 - [cfinclude](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfinclude)
 - [cflocation](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cflocation)
9. [Debugging](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#debugging)
 - [cfdump](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfdump)
 - [cflog](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cflog)
10. [Database](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#database)
 - [cfquery](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfquery)
 - [cftransaction](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cftransaction)
11. [File System Operations](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#file-system-operations)
 - [cfdirectory](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfdirectory)
 - [cffile](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cffile)
12. [Image Manipulation](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#image-manipulation)
 - [cfimage](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfimage)
13. [Spreadsheet Integration](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#spreadsheet-integration)
 - [cfspreadsheet](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfspreadsheet)
14. [Tags Implemented as Components](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#tags-implemented-as-components)
 - [cfquery / query.cfc](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfquery--querycfc)
 - [cfhttp / http.cfc](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfhttp--httpcfc)
 - [cfmail / mail.cfc](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfmail--mailcfc)
 - [cffeed / feed.cfc](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cffeed--feedcfc)
 - [cfftp / ftp.cfc](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfftp--ftpcfc)
15. [Interfaces, Components & Functions](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#interfaces-components--functions)
 - [cfinterface](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfinterface)
 - [cfcomponent](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cfcomponent)
 - [cffunction](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#cffunction)
 - [A More Complete Component Example](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#a-more-complete-component-example)
 - [Annotations](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#annotations)
 - [Function Expressions](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#function-expressions)
16. [Real World Conversions By Example](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#real-world-conversions-by-example)
 - [Example 1](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#example-1)
 - [Example 2](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#example-2)
 - [Example 3](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#example-3)
17. [Tags Have Their Place](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#tags-have-their-place)
 - [Keeping Tags in the View](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#keeping-tags-in-the-view)
 - [Building Tag Code on the Script Side](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#building-tag-code-on-the-script-side)

### The <em>Modern</em> Implementation of Tags to Script

I want to open with this before diving into the depths of conversions. Adobe ColdFusion 11+, Railo 3.2+(?) and Lucee 4.5+ all offer some kind of full script syntax support (Railo & Lucee sharing the implementation) involving <em>near</em> identical syntax between tag-base and script-base. Adobe ColdFusion 11 rolled it's own variation but Railo and Lucee both support ACF's syntax as of versions 4.2 and 4.5 respectively.

As per [Adam Cameron's CFScript Documentation](https://github.com/adamcameron/cfscript/blob/master/cfscript.md#the-rest):
> On Railo/Lucee this is a matter of removing the "`<cf`" and the "`>`", and using normal block syntax (curly braces) where the tag-version is a block-oriented tag.

> On ColdFusion, replace the "`<cftagname`" with "`cftagname(`", and the "`>`" with "`)`", and comma-separate the attributes. Note that this will make the construct look like a function, but it actually is not, and cannot be used like a function, eg this is invalid syntax:

> `result = cfhttp(method="post", url="http://example.com");`

Where the correct way would be: `cfhttp(result="result", method="post", url="http://example.com");`

### Comments

_**Tags:**_
```coldfusion
<!--- I'm a single-line comment. --->

<!---
I'm a multi-
line comment.
--->
```

_**Script:**_
```coldfusion
<cfscript>

// I'm a single-line comment.
// Notice that CFScript code within a ".cfm" file must be wrapped in <cfscript> tags.

/*
I'm a multi-
line comment.
*/

</cfscript>
```

### Variables

_**Tags:**_
```coldfusion
<!--- Some simple variable statements in tags --->

<!--- Default variable declarations --->
<cfparam name="title" default="">
<cfparam name="views" type="numeric" default=0>

<!--- Regular assignment --->
<cfset title = "Tags">
<cfset views = 1>
<cfset page = "Title: #title#, Number: #views#">
```

_**Script:**_
```coldfusion
<cfscript>

// Some simple variable statements in script

// Default variable declarations
param name="title" default="";
param name="views" type="numeric" default=0;

// Regular assignment
title = "Script";
views = 2;
page = "Title: #title#, Number: #views#";
// or
page = "Title: " & title & ", " & "Number: " & views;

</cfscript>
```

### Operators

#### Decision

_**Tags:**_
```coldfusion
<cfset x = 1>
<cfset y = [
	x EQ 1,
	x NEQ 1,
	x LT 1,
	x GT 1,
	x LTE 1,
	x GTE 1
]>
<cfdump var="#y#">
```

_**Script:**_
```coldfusion
<cfscript>

// All tag based operators still work in script
// There are also these equivalents

x = 1;
y = [
	x == 1,
	x != 1,
	x < 1,
	x > 1,
	x <= 1,
	x >= 1
];
writeDump(y);

</cfscript>
```

#### Increment / Decrement

_**Tags:**_
```coldfusion
<!--- Increment --->
<cfset x = 1>
<cfset y = x++>
<cfset z = ++x> <!--- or z = x + 1 --->
<cfdump var="#[x, y, z]#">

<!--- Decrement --->
<cfset x = 1>
<cfset a = x-->
<cfset b = --x> <!--- or b = x - 1 --->
<cfdump var="#[a, b]#">
```

_**Script:**_
```coldfusion
<cfscript>

// Increment
x = 1;
y = x++;
z = ++x // or z = x + 1
writeDump([x, y, z]);

// Decrement
a = x--;
b = --x // or b = x - 1
writeDump([a, b]);

</cfscript>
```

#### Inline Assignment

_**Tags:**_
```coldfusion
<cfset x = 0>
<cfset y = "string">

<cfset x += 10>
<!--- or x = x + 10 --->
<cfdump var="#x#">

<cfset x -= 8>
<!--- or x = x - 8 --->
<cfdump var="#x#">

<cfset x /= 6>
<!--- or x = x / 6 --->
<cfdump var="#x#">

<cfset x *= 4>
<!--- or x = x * 4 --->
<cfdump var="#x#">

<cfset x %= 2>
<!--- or x = x MOD 2 or x = x % 2 --->
<cfdump var="#x#">

<cfset y &= "s">
<!--- or y = y & "s" --->
<cfdump var="#y#">
```

_**Script:**_
```coldfusion
<cfscript>

x = 0;
y = "string";

x += 10;
// or x = x + 10
writeDump(x);

x -= 8;
// or x = x - 8
writeDump(x);

x /= 6;
// or x = x / 6
writeDump(x);

x *= 4;
// or x = x * 4
writeDump(x);

x %= 2;
// or x = x MOD 2 or x = x % 2
writeDump(x);

y &= "s";
// or y = y & "s"
writeDump(x);

</cfscript>
```

#### Boolean

_**Tags:**_
```coldfusion
<cfset x = y = 1>
<cfset z = [
	NOT x,
	x EQ 1 AND y EQ 2,
	x EQ 1 OR y EQ 2
]>
<cfdump var="#z#">
```

_**Script:**_
```coldfusion
<cfscript>

x = y = 1;
z = [
	!x,
	x == 1 && y == 2,
	x == 1 || y == 2
];
writeDump(z);

</cfscript>
```

#### Ternary & Null-Coalescing

_**Tags:**_
```coldfusion
<!--- Ternary --->
<cfset x = "Tags">
<cfset y = len(x) ? x : "something else">
<cfdump var="#y#">

<!--- Null-Coalescing --->
<cfset y = z ?: "something else">
<cfdump var="#y#">
```

_**Script:**_
```coldfusion
<cfscript>

// Ternary
x = "CFScript";
y = len(x) ? x : "something else";
writeDump(y);

// Null-Coalescing
y = z ?: "something else";
writeDump(y);

</cfscript>
```

### Conditions

#### cfif / cfelseif / cfelse

_**Tags:**_
```coldfusion
<cfset count = 10>
<cfif count GT 20>
	<cfoutput>#count#</cfoutput>
<cfelseif count EQ 8>
	<cfoutput>#count#</cfoutput>
<cfelse>
	<cfoutput>#count#</cfoutput>
</cfif>
```

_**Script:**_
```coldfusion
<cfscript>

count = 10;
if (count > 20) {
	writeOutput(count);
} else if (count == 8) {
	writeOutput(count);
} else {
	writeOutput(count);
}

</cfscript>
```

#### cfswitch

_**Tags:**_
```coldfusion
<cfset fruit = "">
<cfswitch expression="#fruit#">
    <cfcase value="Apple">
        <cfoutput>I like apples!</cfoutput>
    </cfcase>
    <cfcase value="Orange">
        <cfoutput>I like oranges!</cfoutput>
    </cfcase>
    <cfcase value="Kiwi">
        <cfoutput>I like kiwi!</cfoutput>
    </cfcase>
    <cfdefaultcase>
        <cfoutput>Fruit, what fruit?</cfoutput>
    </cfdefaultcase>
</cfswitch>
```

_**Script:**_
```coldfusion
<cfscript>

fruit = "";
switch(fruit) {
	case "Apple":
		writeOutput("I like apples!");
	break;
	case "Orange":
		writeOutput("I like oranges!");
	break;
	case "Kiwi":
		writeOutput("I like kiwi!");
	break;
	default:
		writeOutput("Fruit, what fruit?");
	break;
}

</cfscript>
```

#### cftry / cfcatch / cffinally

_**Tags:**_
```coldfusion
<cftry>
	<cfset x = y + z>
	<cfcatch type="any">
		<cfoutput>#cfcatch.message#</cfoutput>
	</cfcatch>
	<cffinally>
		<cfoutput>Finally at the end.</cfoutput>
	</cffinally>
</cftry>
```

_**Script:**_
```coldfusion
<cfscript>

try {
	x = y + z;
}
catch(any e) {
	writeOutput(e.message);
}
finally {
	writeOutput("Finally at the end");
}

</cfscript>
```

#### cfthrow & cfrethrow

_**Tags:**_
```coldfusion
<!--- <cfthrow> --->
<cfthrow message="Oh no an error!!1" type="RealBadErrorException" detail="Something bad happened in detail">

<!--- <cfrethrow> --->
<cfrethrow>
```

_**Script:**_
```coldfusion
<cfscript>

// <cfthrow>
throw(message = "Oh no an error!!1", type = "RealBadErrorException", detail = "Something bad happened in detail");
// throw() can even be as simple as this...
throw "Oh no an error!!1";

// <cfrethrow>
rethrow;

</cfscript>
```

### Iterations

#### General Purpose Loop

_**Tags:**_
```coldfusion
<cfloop index="i" from="1" to="10">
	<cfoutput>#i#</cfoutput>
</cfloop>
```

_**Script:**_
```coldfusion
<cfscript>

for (i = 1; i <= 10; i++) {
	writeOutput(i);
}

</cfscript>
```

#### Array Loop

_**Tags:**_
```coldfusion
<!--- Define our array --->
<cfset myArray = ["a", "b", "c"]>

<!--- By index --->
<cfloop index="i" from="1" to="#arrayLen(myArray)#">
	<cfoutput>#myArray[i]#</cfoutput>
</cfloop>

<!--- By array --->
<cfloop index="currentIndex" array="#myArray#">
	<cfoutput>#currentIndex#</cfoutput>
</cfloop>
```

_**Script:**_
```coldfusion
<cfscript>

// Define our array
myArray = ["a", "b", "c"];

// By index
// Note the use of the newer member function syntax for arrayLen()
for (i = 1; i <= myArray.len(); i++) {
	writeOutput(myArray[i]);
}

// By array
for (currentIndex in myArray) {
	writeOutput(currentIndex);
}

// By arrayEach()
myArray.each(function(element, index) {
	writeOuput(element & " : " & index);
});

</cfscript>
```

#### Struct Loop

_**Tags:**_
```coldfusion
<!--- Define our struct --->
<cfset myStruct = {name: "Tony", state: "Florida"}>

<!--- By struct --->
<cfloop item="currentKey" collection="#myStruct#">
	<cfoutput><li>#currentKey# : #myStruct[currentKey]#</li></cfoutput>
</cfloop>
```

_**Script:**_
```coldfusion
<cfscript>

// Define our struct
myStruct = {name: "Tony", state: "Florida"};

// By struct
for (currentKey in myStruct) {
	writeOutput("<li>#currentKey# : #myStruct[currentKey]#</li>");
}

// By structEach()
myStruct.each(function(key, value) {
	writeOutput("<li>#key# : #value#</li>");
});

</cfscript>
```

#### List Loop

_**Tags:**_
```coldfusion
<!--- Define our list --->
<cfset myList = "a, b, c">

<!--- By list --->
<cfloop index="item" list="#myList#">
	<cfoutput>#item#</cfoutput>
</cfloop>

<!--- By array --->
<cfloop index="currentIndex" array="#listToArray(myList, ",")#">
	<cfoutput>#currentIndex#</cfoutput>
</cfloop>
```

_**Script:**_
```coldfusion
<cfscript>

// Define our list
myList = "a, b, c";

// By array
for (item in listToArray(myList, ",")) {
	writeOutput(item);
}

// By listEach()
myList.each(function(element, index) {
	writeOuput(element & " : " & index);
}, ",");

</cfscript>
```

#### Query Loop

_**Tags:**_
```coldfusion
<!--- Define our query --->
<cfset platform = ["Adobe ColdFusion", "Railo", "Lucee"]>
<cfset myQuery = queryNew("")>
<cfset queryAddColumn(myQuery, "platform", "CF_SQL_VARCHAR", platform)>

<!--- By row index --->
<cfloop index="i" from="1" to="#myQuery.recordCount#">
	<cfoutput><li>#myQuery["platform"][i]#</li></cfoutput>
</cfloop>

<!--- By group --->
<cfloop query="myQuery" group="platform">
	<cfoutput><li>#platform#</li></cfoutput>
</cfloop>
```

_**Script:**_
```coldfusion
<cfscript>

// Define our query
platform = ["Adobe ColdFusion", "Railo", "Lucee"];
myQuery = queryNew("");
queryAddColumn(myQuery, "platform", "CF_SQL_VARCHAR", platform);

// By row index
for (i = 1; i <= myQuery.recordCount; i++) {
    writeOutput("<li>#myQuery["platform"][i]#</li>");
}

// By query
for (row in myQuery) {
    writeOutput("<li>#row.platform#</li>");
}

</cfscript>
```

### Other Flow Control Tags

#### cfabort & cfexit

_**Tags:**_
```coldfusion
<!--- <cfabort> --->
<cfabort statusError="My error message">

<!--- <cfexit> --->
<cfexit method="method">
```

### General

#### cfoutput

_**Tags:**_
```coldfusion
<cfoutput>Some text and a #variable#</cfoutput>
```

_**Script:**_
```coldfusion
<cfscript>

writeOutput("Some text and a #variable#");
// or
writeOutput("Some text and a " & variable);

</cfscript>
```

#### cfsavecontent

_**Tags:**_
```coldfusion
<cfsavecontent variable="myContent">
	<cfoutput>Some content.</cfoutput>
</cfsavecontent>
```

_**Script:**_
```coldfusion
<cfscript>

savecontent variable="myContent" {
	writeOutput("Some content.");
}

</cfscript>
```

#### cfthread

_**Tags:**_
```coldfusion
<cfthread action="run" name="myThread">
	<!--- Do single thread stuff --->
</cfthread>

<cfthread action="join" name="myThread,myOtherThread" />
```

_**Script:**_
```coldfusion
<cfscript>

thread action="run" name="myThread" {
	// do single thread stuff
}

thread action="join" name="myThread,myOtherThread";

</cfscript>
```

#### cflock

_**Tags:**_
```coldfusion
<cflock timeout="60" scope="session" type="exclusive">
	<cfset session.myVar = "Hello">
</cflock>
```

_**Script:**_
```coldfusion
<cfscript>

lock timeout="60" scope="session" type="exclusive" {
	session.myVar = "Hello";
}

</cfscript>
```

#### cfinclude

_**Tags:**_
```coldfusion
<cfinclude template="mypage.cfm">
```

_**Script:**_
```coldfusion
<cfscript>

include "mypage.cfm";

</cfscript>
```

#### cflocation

_**Tags:**_
```coldfusion
<cflocation url="mypage.cfm" addToken="false" statusCode="301">
```

_**Script:**_
```coldfusion
<cfscript>

location("mypage.cfm", "false", "301");

</cfscript>
```

### Debugging

#### cfdump

_**Tags:**_
```coldfusion
<cfdump var="#cgi#" label="CGI Scope">
```

_**Script:**_
```coldfusion
<cfscript>

writeDump(var = cgi, label = "CGI Scope");

</cfscript>
```

#### cflog

_**Tags:**_
```coldfusion
<cflog text="Logging some info." type="information" application="no" file="myLogFile">
```

_**Script:**_
```coldfusion
<cfscript>

writeLog(text = "Logging some info.", type = "information", application = "no", file = "myLogFile");

</cfscript>
```

_**Script:**_
```coldfusion
<cfscript>

// <cfabort>
abort "My error message";

// <cfexit>
exit "method";

</cfscript>
```

### Database

#### cfquery

_**Tags:**_
```coldfusion
<cfquery name="myQuery" datasource="myDSN">
	SELECT myCol1, myCol2 FROM myTable
	WHERE myCol1 = <cfqueryparam value="#myId#" cfsqlype="cf_sql_integer">
	ORDER BY myCol1 ASC
</cfquery>
```

_**Script:**_
```coldfusion
<cfscript>

// Also see the "Tags Implemented as Components" section for another method of using <cfquery> in script

myQuery = queryExecute(
	"SELECT myCol1, myCol2 FROM myTable
	WHERE myCol1 = :myId
	ORDER BY myCol1 ASC",
	{myId: {value: 5, cfsqltype: "cf_sql_integer"}},
	{datasource = "myDSN"}
);

</cfscript>
```

#### cftransaction

_**Tags:**_
```coldfusion
<cftransaction>
<cftry>
	<!--- code to run --->
	<cftransaction action="commit" />
	<cfcatch type="any">
		<cftransaction action="rollback" />
	</cfcatch>
</cftry>
</cftransaction>
```

_**Script:**_
```coldfusion
<cfscript>

transaction {
	try {
		// code to run
		transaction action="commit";
	}
	catch(any e) {
		transaction action="rollback";
	}
}

</cfscript>
```

### File System Operations

#### cfdirectory

_**Tags:**_
```coldfusion
<!--- Directory List --->
<cfdirectory action="list" directory="#expandPath("./")#" recurse="false" name="myList">

<!--- Directory Create --->
<cfdirectory action="create" directory="#expandPath("./new_directory")#">

<!--- Directory Delete --->
<cfdirectory action="delete" directory="#expandPath("./my_directory")#">

<!--- Directory Rename --->
<cfdirectory action="rename" directory="#expandPath("./my_directory")#" newdirectory="#expandPath("./new_directory")#">
```

_**Script:**_
```coldfusion
<cfscript>

// Directory List
myList = directoryList(expandPath("./"), false, "query");

// Directory Create
directoryCreate(expandPath("./new_directory"));

// Directory Delete
directoryDelete(expandPath("./my_directory"));

// Directory Rename
directoryRename(expandPath("./my_directory"), expandPath("./new_driectory"));

</cfscript>
```

#### cffile

_**Tags:**_
```coldfusion
<!--- File Write --->
<cffile action="write" file="#expandPath("./myFile.txt")#" output="Here's some content for my file.">

<!--- File Append --->
<cffile action="append" file="#expandPath("./myFile.txt")#" attributes="normal" output="Here's some new content.">

<!--- File Read --->
<cffile action="read" file="#expandPath("./myFile.txt")#" variable="myFile">

<!--- File Read Binary --->
<cffile action="readBinary" file="#expandPath("./myImage.jpg")#" variable="myImageBinary">

<!--- File Rename --->
<cffile action="rename" source="#expandPath("./myFile.txt")#" destination="#expandPath("./myNewFileName.txt")#" attributes="normal">

<!--- File Copy --->
<cffile action="copy" source="#expandPath("./myFile.txt")#" destination="#expandPath("./some/other/path")#">

<!--- File Move --->
<cffile action="move" source="#expandPath("./myFile.txt")#" destination="#expandPath("./some/other/path")#">

<!--- File Delete --->
<cffile action="delete" file="#expandPath("./myFile.txt")#">

<!--- File Upload --->
<cffile action="upload" destination="#expandPath("./destination)#" filefield="form.myFile" nameconflict="makeunique">

<!--- File Upload All --->
<cffile action="uploadall" destination="#expandPath("./destination")#" nameconflict="makeunique">
```

_**Script:**_
```coldfusion
<cfscript>

// File Write
fileWrite(expandPath("./myFile.txt"), "Here's some content for my file.");

// File Append
// There is no "fileAppend()" so we access the file and use fileWriteLine()
myFile = fileOpen(expandPath("./myFile.txt"), "write");
fileWriteLine(myFile, "Here's some new content.");
fileClose(myFile);

// File Read
myFile = fileRead(expandPath("./myFile.txt"));

// File Read Binary
myImageBinary = fileReadBinary(expandPath("./myImage.jpg"));

// File Rename
// Since there is no "fileRename()", fileMove() works just as well
fileMove(expandPath("./myFile.txt"), expandPath("./myNewFileName.txt"));

// File Copy
fileCopy(expandPath("./myFile.txt"), expandPath("./some/other/path"));

// File Move
fileMove(expandPath("./myFile.txt"), expandPath("./some/other/path"));

// File Delete
fileDelete(expandPath("./myFile.txt"));

// File Upload
fileUpload(expandPath("./destination"), form.myFile, "", "makeunique");

// File Upload All
fileUploadAll(expandPath("./destination"), "", "makeunique");

</cfscript>
```

### Image Manipulation

#### cfimage

> There is <em>quite</em> the lot of image-related functions for &lt;cfimage&gt; that are already decently documented by Adobe. For the sake of avoiding a lengthy bit of repeating, you can check out those functions here - [ColdFusion Wiki: Image Functions](https://wikidocs.adobe.com/wiki/display/coldfusionen/Image+functions)

### Spreadsheet Integration

#### cfspreadsheet

> Much like &lt;cfimage&gt;, &lt;cfspreadsheet&gt; has a fair collection of functions for working with spreadsheets which you can find here - [ColdFusion Wiki: Microsoft Office Integration Functions](https://wikidocs.adobe.com/wiki/display/coldfusionen/Microsoft+office+integration+functions)

### Tags Implemented as Components

#### cfquery / query.cfc

_**Tags:**_
```coldfusion
<cfquery name="myQuery" datasource="myDSN">
	SELECT myCol1, myCol2 FROM myTable
	WHERE myCol1=<cfqueryparam value="#myId#" cfsqlype="cf_sql_integer">
	ORDER BY myCol1 ASC
</cfquery>
```

_**Script:**_
```coldfusion
<cfscript>

myQuery = new Query().setDatasource("myDSN");
myQuery.setSQL("
	SELECT myCol1, myCol2 FROM myTable
	WHERE myCol1=:myId
	ORDER BY myCol1 ASC
");
myQuery.addParam(name: "myCol1", value: "#myId#", cfsqltype: "cf_sql_integer");
myQuery = myQuery.execute().getResult();

</cfscript>
```

#### cfhttp / http.cfc

_**Tags:**_
```coldfusion
<cfhttp result="result" method="GET" charset="utf-8" url="https://www.google.com/">
	<cfhttpparam name="q" type="formfield" value="cfml">
</cfhttp>

<cfdump var="#result#">
```

_**Script:**_
```coldfusion
<cfscript>

httpService = new http(method = "GET", charset = "utf-8", url = "https://www.google.com/");
httpService.addParam(name = "q", type = "formfield", value = "cfml");
result = httpService.send().getPrefix();

writeDump(result);

</cfscript>
```

#### cfmail / mail.cfc

_**Tags:**_
```coldfusion
<cfmail to="your@email.com" from="another@email.com" subject="CFMail Example">
	Your Email Message!!1
</cfmail>
```

_**Script:**_
```coldfusion
<cfscript>

// It's a good idea to build your message inside a save content block first
savecontent variable="mailBody" {
	writeOutput("Your Email Message!!1");
};
// Create and populate the mail object
mailService = new mail(
	to = "your@email.com",
	from = "another@email.com",
	subject = "CFMail Example",
	body = mailBody
);
// Send
mailService.send();

</cfscript>
```

#### cffeed / feed.cfc

_**Tags:**_
```coldfusion
<!--- Read --->
<cffeed
	name="feed"
	action="read"
	source="http://feeds.feedburner.com/ColdfusionbloggersorgFeed?format=xml"
	query="feedQuery"
	properties="feedMetadata"
>
<cfdump var="#feed#">
```

_**Script:**_
```coldfusion
<cfscript>

// Read
feedService = new feed();
feed = feedService.read(
	source = "http://feeds.feedburner.com/ColdfusionbloggersorgFeed?format=xml",
	query = "feedQuery",
	properties = "feedMetadata"
);
writeDump(feed);

</cfscript>
```

#### cfftp / ftp.cfc

_**Tags:**_
```coldfusion
<!--- Open connection --->
<cfftp action="open" connection="myConn" username="myUName" password="myPW" server="ftp.server.com" stopOnError="true">
<!--- Get list of dir --->
<cfftp action="listdir" connection="myConn" name="filesList" directory="/" stopOnError="true">
<!--- Close connection --->
<cfftp action="close" connection="myConn" stopOnError="true">
```

_**Script:**_
```coldfusion
<cfscript>

// Create FTP service and set attributes for connection
ftpService = new ftp(); 
ftpService.setConnection("myConn");
ftpService.setUsername("myUName");
ftpService.setPassword("myPW");
ftpService.setServer("ftp.server.com");
ftpService.setStopOnError(true);
// Open connection
ftpService.open();
// Get list of dir
fileList = ftpService.listdir(directory = "/", stopOnError = true).getResult();
// Close connection
ftpService.close();

</cfscript>
```

### Interfaces, Components & Functions

#### cfinterface

_**Tags:**_
```coldfusion
<cfinterface displayname="My Interface">
	<cfunction name="myFunction" returntype="numeric">
		<cfargument required="true" type="string" name="myArgument">
	</cffunction>
</cfinterface>
```

_**Script:**_
```coldfusion-cfc
interface displayname="My Interface" {
	numeric function myFunction(required string myArgument);
}
```

#### cfcomponent

_**Tags:**_
```coldfusion
<cfcomponent displayname="myComponent" output="false">
	<!--- functions and other values here --->
</cfcomponent>
```

_**Script:**_
```coldfusion-cfc
component displayname="myComponent" output="false" {
	// functions and other values here
}
```

#### cffunction

_**Tags:**_
```coldfusion
<cffunction access="public" returntype="boolean" name="myFunction">
	<cfargument required="true" type="any" name="myArgument">
	
	<!--- Some function bits --->
	
	<cfreturn true>
</cffunction>
```

_**Script:**_
```coldfusion-cfc
public boolean function myFunction(required any myArgument) {
	// Some function bits
	
	return true;
}
```

#### A More Complete Component Example

_**Tags:**_
```coldfusion
<cfcomponent displayname="Utils" output="false">
	<cfproperty name="version" type="string" default="0.0.1">

	<cffunction access="public" returntype="string" name="doReverse" hint="I reverse the supplied string">
		<cfargument required="true" type="string" name="stringToReverse">
		
		<cfreturn reverse(arguments.stringToReverse)>
	</cffunction>
	
	<cffunction access="public" returntype="array" name="reverseArrayOrder">
		<cfargument type="array" name="arrayToReverse" default="#["Adobe ColdFusion", "Lucee", "Railo"]#" hint="I reverse an array's order">
		
		<cfset var result = []>
		<cfset var i = 0>
		<cfloop index="i" from="#arrayLen(arguments.arrayToReverse)#" to="1" step="-1">
			<cfset arrayAppend(result, arguments.arrayToReverse[i])>
		</cfloop>
		
		<cfreturn result>
	</cffunction>
</cfcomponent>
```

_**Script:**_
```coldfusion-cfc
component displayname="Utils" output="false" {
	property name="version" type="string" default="0.0.1";

	public string function doReverse(required string stringToReverse)
		hint="I reverse the supplied string"
	{
		return reverse(arguments.stringToReverse);
	}
	
	public array function reverseArrayOrder(array arrayToReverse = ["Adobe ColdFusion", "Lucee", "Railo"])
		hint="I reverse an array's order"
	{
		var result = [];
		for (var i = arrayLen(arguments.arrayToReverse); i >= 1; i--) {
			result.append(arguments.arrayToReverse[i]);
		}
		
		return result;
	}
}
```

#### Annotations

> Information about a script-based component, property or function - it's attributes & arguments can be defined via the annotation syntax.

_**Script:**_
```coldfusion-cfc
// Consider this code...

public numeric function adder(required numeric x, required numeric y)
	hint="I add things"
{
	return arguments.x + arguments.y;
}

// Now with annotations

/**
* @returnType numeric
* @hint I add things
*/
public function adder(required numeric x, required numeric y) {
	return arguments.x + arguments.y;
}
```

#### Function Expressions

> Consider the tag-based version of the function below. In CFScript, we can instead define a variable with an anonymous function that does the same task.

_**Tags:**_
```coldfusion
<cffunction access="public" returntype="numeric" name="adder">
	<cfargument required="true" type="numeric" name="x">
	<cfargument required="true" type="numeric" name="y">
	
	<cfreturn arguments.x + arguments.y>
</cffunction>

<cfoutput>#adder(2, 2)#</cfoutput>
```

_**Script:**_
```coldfusion
<cfscript>

adder = function(x, y) {
	return x + y;
};

writeOutput(adder(2, 2));

// You can be more specific with type, scope, required etc.
adder = function(required numeric x, required numeric y) {
	return arguments.x + arguments.y;
};

writeOutput(adder(2, "a")); // this errors

</cfscript>
```

### Real World Conversions By Example

> ##### The below examples are pieces of code found from online/offline sources. Anything with a name on it will be given credit and/or linked accordingly. If you see your code as an example and you don't want it here, LET ME KNOW! Cheers. - @cfchef

#### Example 1

> Here's a function, written in tags, picked out from CFLib.org - [_utcOffsetToMinutes() by Mosh Teitelbaum_](http://www.cflib.org/udf/utcOffsetToMinutes)

_**Tags:**_
```coldfusion
<!---
Converts UTC Offset to minutes.

@param offset The formatted UTC offset to be converted to minutes. (Required)
@return Returns a number.
@author Mosh Teitelbaum (mosh.teitelbaum@evoch.com)
@version 1, 1/8/2015
--->

<cffunction name="utcOffsetToMinutes" returntype="numeric" output="no" description="Converts UTC Offset to minutes.">
	<cfargument name="offset" type="string" required="yes" hint="The formatted UTC offset to be converted to minutes.">

	<!--- Initialize local variables --->
	<cfset var h = 0>	<!--- hours --->
	<cfset var m = 0>	<!--- minutes --->
	<cfset var s = 1>	<!--- sign --->
	<cfset var str = ReReplaceNoCase(arguments.offset, "[^-:0-9]", "", "ALL")>	<!--- offset with non-important characters removed --->

	<!--- If first character is "-", adjust sign --->
	<cfif Compare(Left(str, 1), "-") EQ 0>
		<cfset s = -1>
		<cfset str = Right(str, Len(str) - 1)>
	</cfif>

	<!--- Determine number of hours and minutes --->
	<cfif ListLen(str, ":") EQ 2>
		<cfset h = ListFirst(str, ":")>
		<cfset m = ListLast(str, ":")>
	<cfelseif Len(str) EQ 2>
		<cfset h = str>
	<cfelseif Len(str) EQ 3>
		<cfset h = Left(str, 1)>
		<cfset m = Right(str, 2)>
	<cfelseif Len(str) EQ 4>
		<cfset h = Left(str, 2)>
		<cfset m = Right(str, 2)>
	</cfif>

	<!--- Return number of minutes --->
	<cfreturn s * ((h * 60) + m)>
</cffunction>
```

_**Script:**_
```coldfusion
<cfscript>

/**
* @hint Converts UTC Offset to minutes.
* @param offset The formatted UTC offset to be converted to minutes. (Required)
* @return Returns a number.
* @author Mosh Teitelbaum (mosh.teitelbaum@evoch.com)
* @version 1, 1/8/2015
*/
public numeric function utcOffsetToMinutes(required string offset) {
	// Initialize local variables
	var h = 0; // hours
	var m = 0; // minutes
	var s = 1; // sign
	var str = reReplaceNoCase(arguments.offset, "[^-:0-9]", "", "ALL"); // offset with non-important characters removed

	// If first character is "-", adjust sign
	if (compare(left(str, 1), "-") == 0) {
		s = -1;
		str = right(str, len(str) - 1);
	}

	// Determine number of hours and minutes
	if (listLen(str, ":") == 2) {
		h = listFirst(str, ":");
		m = listLast(str, ":");
	} else if (len(str) == 2) {
		h = str;
	} else if (len(str) == 3) {
		h = left(str, 1);
		m = right(str, 2);
	} else if (len(str) == 4) {
		h = left(str, 2);
		m = right(str, 2);
	}

	// Return number of minutes
	return s * ((h * 60) + m);
}

</cfscript>
```

#### Example 2

> Here's another one from CFLib.org - [_addRemoveDebuggingIPAddress() by Qasim Rasheed_](http://www.cflib.org/udf/addRemoveDebuggingIPAddress)

_**Tags:**_
```coldfusion
<!---
 This function will either add or remove an IP address to the list of debugging ip addresses if you do not have an administrator access.
 
 @param ipAddress 	 IP Address (Required)
 @param action 	 Add or Remove. Defaults to Add. (Optional)
 @return Returns a list of IP addresses. 
 @author Qasim Rasheed (qasim_1976@yahoo.com) 
 @version 1, February 17, 2004 
--->
<cffunction name="addRemoveDebuggingIPAddress" output="false" returnType="string">
	<cfargument name="IPaddress" type="string" required="Yes" />
	<cfargument name="action" type="string" default="Add" />
	<cfscript>
		var factory = CreateObject("Java","coldfusion.server.ServiceFactory");
		var debuggingService = "";
	</cfscript>
	<cflock name="factory_debuggingservice" type="exclusive" timeout="5">
		<cfset debuggingService = factory.getDebuggingService()>
		<cfswitch expression="#arguments.action#">
			<cfcase value="Add">
				<cfif not listcontainsnocase(debuggingService.iplist.ipList,arguments.IPaddress)>
					<cfset debuggingService.iplist.ipList = ListAppend(debuggingService.iplist.ipList,arguments.IPaddress)>
				</cfif>
			</cfcase>
			<cfcase value="Remove">
				<cfif listcontainsnocase(debuggingService.iplist.ipList,arguments.IPaddress)>
					<cfset debuggingService.iplist.ipList = ListDeleteAt(debuggingService.iplist.ipList,ListFindNoCase(debuggingService.iplist.ipList,arguments.IPaddress))>
				</cfif>
			</cfcase>
		</cfswitch>
		<cfreturn debuggingService.iplist.ipList />
	</cflock>
</cffunction>
```

_**Script:**_
```coldfusion
<cfscript>

/**
* @hint This function will either add or remove an IP address to the list of debugging ip addresses if you do not have an administrator access.
* @param ipAddress IP Address (Required)
* @param action Add or Remove. Defaults to Add. (Optional)
* @return Returns a list of IP addresses. 
* @author Qasim Rasheed (qasim_1976@yahoo.com) 
* @version 1, February 17, 2004 
*/
public string function addRemoveDebuggingIPAddress(required string IPaddress, string action = "Add")
	output="false"
{
	var factory = createObject("java","coldfusion.server.ServiceFactory");
	var debuggingService = "";
	lock name="factory_debuggingservice" type="exclusive" timeout="5" {
		debuggingService = factory.getDebuggingService();
		switch(arguments.action) {
			case "Add":
				if (!listContainsNoCase(debuggingService.iplist.ipList,arguments.IPaddress)) {
					debuggingService.iplist.ipList = listAppend(debuggingService.iplist.ipList, arguments.IPaddress);
				}
			break;
			case "Remove":
				if (listContainsNoCase(debuggingService.iplist.ipList, arguments.IPaddress)) {
					debuggingService.iplist.ipList = listDeleteAt(debuggingService.iplist.ipList, listFindNoCase(debuggingService.iplist.ipList, arguments.IPaddress));
				}
			break;
		}
		
		return debuggingService.iplist.ipList;
	}
}

</cfscript>
```

#### Example 3

> Yet another example from CFLib.org - [_collectFiles() by Steven Ross_](http://www.cflib.org/udf/collectFiles)

_**Tags:**_
```coldfusion
<!---
 Scans a directory (or path) for files of a specified extension and then copies them to the path you specify.
 v2 by Raymond Camden. I just cleaned up the var statements.
 
 @param extensions 	 List of extensions to copy. (Required)
 @param destinationPath 	 Destination directory. (Required)
 @param sourcePath 	 Source directory. (Required)
 @return Returns nothing. 
 @author Steven Ross (steven.ross@zerium.com) 
 @version 2, April 7, 2006 
--->
<cffunction name="collectFiles" access="public" hint="recurses through a directory and collects the file types you want then outputs to another directory" returnType="void">
	<cfargument name="extensions" required="true" type="string" hint="The extensions you want to gather up csv (list) format ex:(asp,cfm,jsp) ">
	<cfargument name="destinationPath" required="true" type="string" hint="absolute path to storage directory">
	<cfargument name="sourcePath" required="true" type="string" hint="absolute path to source directory">
	<cfset var root = arguments.sourcePath/>
	<cfset var i = "">
	<cfset var absPath = "">
	<cfset var relativePath = "">
	<cfset var writeTo = "">
	<cfset var pathAndFile = "">
	
	<cfif not directoryExists(arguments.sourcePath)>
		<cfthrow message="Source Directory (#arguments.sourcePath#) not found" detail="You didn't pass in a valid source directory, check the path and try again.">
	</cfif>
	
	<cfloop list="#arguments.extensions#" index="i">
		<cfdirectory name="getFiles" directory="#root#" recurse="true" filter="*.#i#">
		<cfloop query="getFiles">
			<cfset absPath = getFiles.directory & "/" />
			<cfset relativePath = Replace(absPath, root, "", "all") />
			<cfset writeTo = ARGUMENTS.destinationPath & "/" & relativePath>
			<cfset pathAndFile = getFiles.directory & "/" & getFiles.name />
			<cfif not directoryExists(writeTo)>
				<cfdirectory action="create" directory="#writeTo#">
				<cffile action="copy" source="#pathAndFile#" destination="#writeTo#">
			<cfelse>
				<cffile action="copy" source="#pathAndFile#" destination="#writeTo#">
			</cfif>
		</cfloop>
	</cfloop>
</cffunction>
```

_**Script:**_
```coldfusion
<cfscript>

/**
* @hint Scans a directory (or path) for files of a specified extension and then copies them to the path you specify.
* @param extensions List of extensions to copy. (Required)
* @param destinationPath Destination directory. (Required)
* @param sourcePath Source directory. (Required)
* @return Returns nothing.
* @author Steven Ross (steven.ross@zerium.com) - v2 by Raymond Camden. I just cleaned up the var statements.
* @version 2, April 7, 2006
*/
public void function collectFiles(required string extensions, required string destinationPath, required string sourcePath) {
	var root = arguments.sourcePath;
	if (!directoryExists(arguments.sourcePath)) {
		throw(
			message = "Source Directory (#arguments.sourcePath#) not found",
			detail = "You didn't pass in a valid source directory, check the path and try again."
		);
	}
	for (var ext in listToArray(arguments.extensions)) {
		var list = directoryList(path = root, recurse = true, listinfo = "query", filter = "*.#ext#");
		for (var dir in list) {
			var absPath = dir.directory & "/";
			var relativePath = replace(absPath, root, "", "all");
			var writeTo = arguments.destinationPath & "/" & relativePath;
			var pathAndFile = dir.directory & "/" & dir.name;
			if (!directoryExists(writeTo)) {
				directoryCreate(writeTo);
				fileCopy(pathAndFile, writeTo);
			} else {
				fileCopy(pathAndFile, writeTo);
			}
		}
	}
}

</cfscript>
```

### Tags Have Their Place

#### Keeping Tags in the View

> The modern CFML world has evolved with various flavors and mixes of Model View Controller (MVC) & Object Oriented Programming (OOP) practices. While procedural coding might have a place, larger applications often call for a more organized, structured collection of functions and how and where they display their results. As opposed to being <em>all</em> in one file, database calls should reside in their own file (Model), structuring/manipulation of that data can be built in a seperate file based on user supplied variables (Controller) and then that structured data is formatted with HTML for display (View).

> From a general standpoint, the view layer should be the home for basic tag functions to help iterate and organize received result data; to be married with your HTML and displayed to the user. Simple tags such as `<cfset>`, `<cfparam>`, `<cfoutput>`, `<cfif>` & `<cfloop>`. With the involvement of HTML in the view, tags make sense as they work with the flow of the layout; leaving your Model and Controllers to be uncluttered and have a clean flow of their own in CFScript. It might be a matter of opinion but you will eventually grow to find this separation quite refreshing visually and mentally when scanning through large blocks of logic vs display code.

Consider this general mock breakdown of code presenting blog posts to the user. This would normally be handled more effectively & efficiently in a MVC framework like [FW/1](http://framework-one.github.io/) or [Coldbox](http://www.coldbox.org/).

_**Model: BlogService.cfc**_

```coldfusion-cfc
/**
* @hint I contain blog related utilities
*/
component displayname="Blog Service"
	output="false"
{
	/**
	* @hint I intiate the service object by setting the datasource
	*/
	public BlogService function init(required string dsn) {
		variables.dsn = arguments.dsn;
		
		return this;
	}
	
	/**
	* @hint I return a query of blog posts
	*/
	public query function getPosts() {
		var qry = new Query();
		qry.setDatasource(variables.dsn);
		qry.setSQL("
			SELECT postId, postTitle, postBody, author, publishDate
			FROM posts
			ORDER BY postId DESC
		");
		
		return qry.execute().getResult();
	}
}
```

_**Controller: BlogController.cfc**_

```coldfusion-cfc
/**
* @hint I receive user request and translate them into response
*/
component displayname="Blog Controller"
	output="false"
{
	/**
	* @hint I initiate the BlogController and call in all required objects
	*/
	public BlogController funtion init() {
		var DataService = createObject("component", "model.services.DataService").init();
		variables.BlogService = createObject("component", "model.services.BlogService").init(DataService.getDSN());
		
		return this;
	}
	
	/**
	* @hint I return a formatted collection of blog posts for display
	*/
	public struct function posts() {
		// Define out request context struct for holding data to pass on to the view
		var rc = {};
		var postQry = variables.BlogService.getPosts();
		// Let's make a friendlier collection as a array of structs of the data
		rc.posts = [];
		if (postQuery.recordCount) {
			for (var post in postQry) {
				arrayAppend(rc.posts, {
					title: post.postTitle,
					body: post.postBody,
					author: post.author,
					published: post.publishDate
				});
			}
		}
		
		return rc;
	}
}
```

_**View: posts.cfm**_

```coldfusion
<cfparam name="rc.posts" default="#[]#">

<cfset BlogController = createObject("component", "blog.controllers.BlogController").init()>
<cfset rc.posts = BlogController.posts()>

<h1>Welcome to my Blog!</h1>
<cfif arrayLen(rc.posts)>
	<div class="post-content">
	<cfoutput>
	<cfloop index="post" array="#rc.posts#">
		<h2>#post.title#</h2>
		<div class="post-meta">Published on: #post.published# By: #post.author#</div>
		<div class="post-body">#post.body#</div>
	</cfloop>
	</cfoutput>
	</div>
<cfelse>
	<h3>No posts to display!</h3>
</cfif>
```

#### Building Tag Code on the Script Side

> While we generally want to keep our presentation layer separate from our business logic, as briefly portrayed in [Keeping Tags in the View](https://github.com/cfchef/cfml-tag-to-script-conversions/blob/master/README.md#keeping-tags-in-the-view), there are some scenarios where we need to do string-building in a function, or similar, to later pass on for an alternate method of viewing in HTML, XML, email etc.

Consider these examples. . .

_**Email - Tags**_

```coldfusion
<!--- Dummy blog post --->
<cfset post = {
	title: "My New Blog Post!",
	slug: "my-new-blog-post",
	body: "Some body content for the post.",
	publishDate: "{ts '2015-07-06 18:17:01'}"
}>

<!--- Build our email --->
<cfsavecontent variable="mailBody">
	<cfoutput>
		<h4>A New Article Has Been Posted @ myblog.com!</h4>
		<h6>#post.title#</h6>
		<p><b>Posted on:</b> #dateFormat(post.publishDate, "YYYY/MM/DD")#</p>
		<p>
			<cfif len(post.body) GT 500>
				#left(post.body, 500)#. . .
			<cfelse>
				#post.body#
			</cfif>
		</p>
		<a href="http://myblog.com/blog/#post.slug#"><b>Read more...</b></a>
	</cfoutput>
</cfsavecontent>

<!--- Send email to subscribers --->
<cfloop item="subscriber" collection="#SubscriberService.getSubscribers()#">
	<cfmail
		type="html"
		to="#subscriber.getEmail()#"
		from="no-reply@myblog.com"
		subject="New Blog Post from MyBlog.com"
		body="#mailBody#"
	>
</cfloop>
```

_**Email - Script**_

```coldfusion
<cfscript>

// Dummy blog post
post = {
	title: "My New Blog Post!",
	slug: "my-new-blog-post",
	body: "Some body content for the post.",
	publishDate: "{ts '2015-07-06 18:17:01'}"
};

// Build our email
savecontent variable="mailBody" {
	writeOutput('
		<h4>A New Article Has Been Posted @ myblog.com!</h4>
		<h6>#post.title#</h6>
		<p><b>Posted on:</b> #dateFormat(post.publishDate, "YYYY/MM/DD")#</p>
		<p>
			if (len(post.body) > 500) {
				#left(post.body, 500)#. . .
			} else {
				#post.body#
			}
		</p>
		<a href="http://myblog.com/blog/#post.slug#"><b>Read more...</b></a>
	');
};

// Send email to subscribers
for (subscriber in SubscriberService.getSubscribers()) {
	mailService = new mail(
		type = "html",
		to = subscriber.getEmail(),
		from = "no-reply@myblog.com",
		subject = "New Blog Post from MyBlog.com!",
		body = encodeForHTML(mailBody)
	);
	mailService.send();
}

</cfscript>
```


_**XML Sitemap - Tags**_

```coldfusion
<!--- Dummy links --->
<cfset links = [
	"http://myblog.com",
	"http://myblog.com/about",
	"http://myblog.com/blog",
	"http://myblog.com/blog/my-blog-post"
]>

<cftry>
	<!--- Build XML --->
	<cfsavecontent variable="xmlData">
	<cfoutput>
		<?xml version="1.0" encoding="UTF-8"?>
		<urlset
			xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
			xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9
			http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd">
		<cfloop index="link" array="#links#">
			<url>
			  <loc>#link#</loc>
			  <changefreq>weekly</changefreq>
			  <priority>0.8</priority>
			</url>
		</cfloop>
		</urlset>
	</cfoutput>
	</cfsavecontent>
	
	<!--- Write to file --->
	<cffile action="write" file="#expandPath("./Sitemap.xml")#" output="#xmlData#">

	<cfcatch type="any">
		<cfoutput>#cfcatch.message#</cfoutput>
	</cfcatch>
</cftry>
```

_**XML Sitemap - Script**_

```coldfusion
<cfscript>

// Dummy links
links = [
	"http://myblog.com",
	"http://myblog.com/about",
	"http://myblog.com/blog",
	"http://myblog.com/blog/my-blog-post"
];

try {
	// Build XML
	savecontent variable="xmlData" {
		writeOutput('
			<?xml version="1.0" encoding="UTF-8"?>
			<urlset
				xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
				xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
				xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9
				http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd">
		');
		for (link in links) {
			writeOutput('
				<url>
				  <loc>#link#</loc>
				  <changefreq>weekly</changefreq>
				  <priority>0.8</priority>
				</url>
			');
		}
		writeOutput('
			</urlset>
		');
	}
	// Write to file
	fileWrite(expandPath("./Sitemap.xml"), xmlData);
}
catch(any e) {
	writeOutput(e.message);
}

</cfscript>
```

## LICENSE
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">CFML Tag to Script Conversions</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://tonyjunkes.com/blog/leave-your-tags-at-the-door-some-cfml-tag-to-script-documentation" property="cc:attributionName" rel="cc:attributionURL">Tony Junkes</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
