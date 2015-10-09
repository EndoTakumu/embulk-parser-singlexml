# Singlexml parser plugin for Embulk

embulkを使用して、xmlから好きな名前でカラムを作成する<br>
※まだ1レコードしか作成できない※

## Overview

* **Plugin type**: parser
* **Guess supported**: no

## Example

```yaml
in:
  type: file
  path_prefix: input.xml
  parser:
   type: singlexml
   schema:
   - {name: name1, type: string, exp: "doc.elements['root/a'].text"}
   - {name: name2, type: string, exp: "doc.elements['root/a/b'].text"}
exec: {}
out:
 type: stdout
```