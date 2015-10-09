# Singlexml parser plugin for Embulk

embulkを使用して、xmlから好きな名前でカラムを作成する<br>
※まだ1レコードしか作成できない※

## Overview

* **Plugin type**: parser
* **Guess supported**: no

## Example

*input.xml
```yaml
<root>
    <a>
        <a_b>a_b</a_b>
        <c>
            <a_c_d1>acd1</a_c_d1>>
            <a_c_d2>acd2</a_c_d2>>
        </c>
    </a>    
</root>
```
*config.yml
```yaml
in:
  type: file
  path_prefix: input.xml
  parser:
   type: singlexml
   schema:
   - {name: a_name1, type: string, exp: "doc.elements['root/a/a_b'].text"}
   - {name: c_name2, type: string, exp: "doc.elements['root/a/c/a_c_d2'].text"}
exec: {}
out:
 type: stdout
```
```yaml
*preview
+----------------+----------------+
| a_name1:string | c_name2:string |
+----------------+----------------+
|            a_b |           acd2 |
+----------------+----------------+
```