# rsdlGenerator

rsdlGenerator - is a program for generation [RSDL](https://en.wikipedia.org/wiki/RSDL) according to api structure.
## Descriptions
rsdlGenerator written in [perl](https://www.perl.org/).
To start program:
```sh
$ perl RSDLGenerator.pl
```
To see available options:
```sh
$ perl RSDLGenerator.pl -help
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
Example of generated RSDL file:
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
    <link rel="get" href="/ACL/get_acl_list">
      <request>
        <http_method>GET</http_method>
        <headers />
        <url>
          <parameters_set>
            <parameter context="query" type="xs:string" required="false">
              <name>group</name>
              <value />
            </parameter>
          </parameters_set>
        </url>
      </request>
    </link>
  </links>
</rsdl>
```
Example of generated RSDL Schema file:
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
 </xs:schema> 
```
