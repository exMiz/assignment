# RGen: RSDL Generator
> Think different. Generate difference. ```Bohdan Butko```

RGen - is a program for generation [RSDL](https://en.wikipedia.org/wiki/RSDL) according to api structure to your api.
[Example](#This)
## Descriptions
RGen written in [perl](https://www.perl.org/).
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
Example RSDL file:
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
