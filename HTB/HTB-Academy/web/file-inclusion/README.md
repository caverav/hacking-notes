# File inclusion notes of htb-academy

## Local File Inclusion (LFI)

Functions comparison for LFI:

| Function       | Read Content | Execute | Remote URL |
|----------------|--------------|---------|------------|
| PHP            |              |         |            |
| include()/include_once() | ✅ | ✅ | ✅ |
| require()/require_once() | ✅ | ✅ | ❌ |
| file_get_contents() | ✅ | ❌ | ✅ |
| fopen()/file() | ✅ | ❌ | ❌ |
| NodeJS         |              |         |            |
| fs.readFile()  | ✅ | ❌ | ❌ |
| fs.sendFile()  | ✅ | ❌ | ❌ |
| res.render()   | ✅ | ✅ | ❌ |
| Java           |              |         |            |
| include        | ✅ | ❌ | ❌ |
| import         | ✅ | ✅ | ✅ |
| .NET           |              |         |            |
| @Html.Partial() | ✅ | ❌ | ❌ |
| @Html.RemotePartial() | ✅ | ❌ | ✅ |
| Response.WriteFile() | ✅ | ❌ | ❌ |
| include        | ✅ | ✅ | ✅ |

### Special implementations

**Prefix**:
```php
include("lang_" . $_GET['language']);
```
In this case it's necessary to prefix an /, por ex: /../../../etc/passwd

**Appended extensions**
```php
include($_GET['language'] . ".php");
```

### Second order attacks
This occurs because many web application functionalities may be insecurely pulling files from the back-end server based on user-controlled parameters.

For example, a web application may allow us to download our avatar through a URL like (/profile/$username/avatar.png). If we craft a malicious LFI username (e.g. ../../../etc/passwd), then it may be possible to change the file being pulled to another local file on the server and grab it instead of our avatar.
