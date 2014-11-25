# `xmlwriter`: functions module for [shellfire]

This module provides a simple framework for writing XML to standard out in a [shellfire] application.

## Overview

The functions are trivial to use. For example, to create the following XML (without line feeds, in reality):-
```xml
<?xml version="1.0" charset="UTF-8"?>
<!DOCTYPE comps PUBLIC "-//CentOS//DTD Comps info//EN" "comps.dtd">
<comps>
	<group project="sw&lt;&gt;ddle">
		<id>groupId</id>
		<name>groupName</name>
		<description>All available packages for 'groupName'</description>
		<default value="false"/>
		<uservisible value="false">TEXT</uservisible>
	</group>
</comps>
```

Use the code:-

```bash
xmlwriter_declaration '1.0' 'UTF-8' 'no'
xmlwriter_dtd comps "-//CentOS//DTD Comps info//EN"
xmlwriter_open comps
	xmlwriter_open group project sw<>ddle
		xmlwriter_leaf id "groupId"
		xmlwriter_leaf name "groupName"
		xmlwriter_leaf description "All available packages for 'groupName'"
		xmlwriter_leaf default value false
		xmlwriter_leaf uservisible value false TEXT
	xmlwriter_close group
xmlwriter_close comps
```

To use namespaces in XML, simply make the node name the namespace prefix, eg `namespace:comps`. We don't care one way or the other.

## Importing

To import this module, add a git submodule to your repository. From the root of your git repository in the terminal, type:-
```bash
mkdir -p lib/shellfire
cd lib/shellfire
git submodule add "https://github.com/shellfire-dev/xmlwriter.git"
cd -
git submodule init --update
```

You may need to change the url `https://github.com/shellfire-dev/xmlwriter.git` above if using a fork.

You will also need to add paths - include the module [paths.d].

## Namespace `xmlwriter`

This namespace exposes helper functions to create an XML document.

### To use in code

If calling from another [shellfire] module, add to your shell code the line
```bash
core_usesIn xmlwriter
```
in the global scope (ie outside of any functions). A good convention is to put it above any function that depends on functions in this module. If using it directly in a program, put this line _inside_ the `_program()` function:-

```bash
_program()
{
	core_usesIn xmlwriter
	…
}
```

### Functions

***
#### `xmlwriter_declaration`

|Parameter|Value|Optional|
|---------|-----|--------|
|`version`|XML version. Version `1.0` is preferred by most consumers.|_No_|
|`encoding`|IANA content type; `UTF-8` should always be specified.|_No_|
|`standalone`|Boolean.|_No_|

Writes an XML declaration to standard out.

***
#### `xmlwriter_dtd`

|Parameter|Value|Optional|
|---------|-----|--------|
|`name`|DTD name|_No_|
|`path`|DTD path|_No_|

Writes an XML DTD to standard out.

***
#### `xmlwriter_open`

|Parameter|Value|Optional|
|---------|-----|--------|
|`nodeName`|XML node name|_No_|
|`…`|Attribute Name-Value string pairs|_Yes_|

Writes an XML opening tag of `nodeName`, with attributes as the XML encoded form of the UTF-8 encoded strings of attribute and value to standard out.


***
#### `xmlwriter_close`

|Parameter|Value|Optional|
|---------|-----|--------|
|`nodeName`|XML node name|_No_|

Writes an XML closing tag of `nodeName` to standard out.


***
#### `xmlwriter_leaf`

|Parameter|Value|Optional|
|---------|-----|--------|
|`nodeName`|XML node name|_No_|
|`…`|Attribute Name-Value string pairs|_Yes_|
|`text`|Node text value|_Yes_|

Writes a leaf XML node of `nodeName`, with attributes as the XML encoded form of the UTF-8 encoded strings of attribute and value. If `text` is supplied, writes it as the text content of the node (even if empty) to standard out. Otherwise writes a self-closed node to standard out.


[RFC 3986]: https://tools.ietf.org/html/rfc3986 "RFC 3986"
[RFC 6570]: http://tools.ietf.org/html/rfc6570 "RFC 6570"
[swaddle]: https://github.com/raphaelcohn/swaddle "Swaddle homepage"
[shellfire]: https://github.com/shellfire-dev "shellfire homepage"
[core]: https://github.com/shellfire-dev/core "shellfire core module homepage"
[paths.d]: https://github.com/shellfire-dev/paths.d "paths.d shellfire module homepage"
[github api]: https://github.com/shellfire-dev/github "github shellfire module homepage"
[jsonwriter]: https://github.com/shellfire-dev/jsonwriter "jsonwriter shellfire module homepage"
[jsonreader]: https://github.com/shellfire-dev/jsonreader "jsonreader shellfire module homepage"
[xmlwriter]: https://github.com/shellfire-dev/xmlwriter "xmlwriter shellfire module homepage"
[unicode]: https://github.com/shellfire-dev/unicode "unicode shellfire module homepage"
[version]: https://github.com/shellfire-dev/version "version shellfire module homepage"
