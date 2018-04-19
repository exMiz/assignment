# rsdlGenerator
rsdlGenerator - is a program for generating [RSDL](https://en.wikipedia.org/wiki/RSDL) according to api structure.

## Description
rsdlGenerator and its modules written in [perl](https://www.perl.org/).

File name           | Description
--------------------|----------------------
`rsdlGenerator.pl`  | Main script for RSDL creating 
`Resource.pm`       | Describes resource of api {name and method_list}
`ResourceMethod.pm` | Describes resource method with {name, input and output data}  
`MethodParams.pm`   | Describes method param with {name, type and mandatory}
`PortaSchema.pm`    | Module that contains hash with api structure
`RSDL.pm`           | Module that contains methods for generating RSDL file and schema
`RSDL_Template.tt`  | Template for RSDL file
`RSDL_Schema.tt`    | Template for RSDL Schema

To start program:
```sh
$ perl rsdlLGenerator.pl
```
To see help:
```sh
$ perl rsdlGenerator.pl -help
```
Default logging level - INFO.
To start verbose logging:
```sh
$ perl rsdlGenerator.pl -v
```

## Example
Module PortaSchema contains variable PORTA_SCHEMA that describes api structure.
```perl
$PORTA_SCHEMA = { 
    'api_service_list' => [
                            {
                              'method_list' => [
                                                 {
                                                   'input' => [
                                                                {
                                                                  'mandatory' => 0,
                                                                  'name' => 'name',
                                                                  'type' => 'string'
                                                                }
                                                              ],
                                                   'name' => 'get_user_id',
                                                   'output' => {
                                                                 'mandatory' => 0,
                                                                 'name' => undef,
                                                                 'object_field_list' => [
                                                                                          {
                                                                                            'mandatory' => 0,
                                                                                            'name' => 'id',
                                                                                            'type' => 'int'
                                                                                          }
                                                                                        ],
                                                                 'type' => 'object',
                                                                 'xsd_type' => 'GetUserId'
                                                               }
                                                 }
                                               ],
                              'name' => 'Users'
                            }
                          ]
                };
```

Example of generated RSDL file (api.rsdl):
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rsdl href="/rsdl" rel="rsdl">
  <description />
  <version major="1" minor="1" build="0" revision="0"/>
  <schema href="/schema" rel="schema">
    <name>api_schema.xsd</name>
    <description />
  </schema>
  <links>
    <link rel="get" href="/Users/get_user_id">
      <request>
        <http_method>GET</http_method>
        <headers />
        <url>
          <parameters_set>
            <parameter context="query" type="xs:string" required="false">
              <name>name</name>
              <value />
            </parameter>
          </parameters_set>
        </url>
      </request>
      <response>
        <type>GetUserId</type>
      </response>
    </link>
  </links>
</rsdl>
```

Example of generated RSDL Schema file (api_schema.xsd):
```xml
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <xs:element name="rsdl">
    <xs:complexType>
      <xs:sequence>
        <xs:element type="xs:string" name="description"/>
        <xs:element ref="version"/>
        <xs:element ref="schema"/>
        <xs:element ref="links"/>
      </xs:sequence>
      <xs:attribute type="xs:string" name="href"/>
      <xs:attribute type="xs:string" name="rel"/>
    </xs:complexType>
  </xs:element>
 ...
   <xs:complexType name="GetUserId">
    <xs:sequence>
      <xs:element type="xs:int" name="id" minOccurs="0"/>
    </xs:sequence>
  </xs:complexType>
 ...
 </xs:schema> 
```
