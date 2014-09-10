write-file-atomic
-----------------

This is an extension for node's `fs.writeFile` that makes its operation
atomic allows you to include uid/gid for the final file as well.  It does
this by initially writing to a temporary file (your filename, followed by
".writeFile.atomic"), chowning it to the uid and gid you specified (if you
specified any) and finally renames it to your filename.

### var writeFileAtomic = require('write-file-atomic')<br>writeFileAtomic(filename, data, [options], callback)

* filename **String**
* data **String** | **Buffer**
* options **Object**
  * chown **Object**
    * uid **Number**
    * gid **Number**
  * encoding **String** | **Null** default = 'utf8'
  * mode **Number** default = 438 (aka 0666 in Octal)
callback **Function**

Atomically and asynchronously writes data to a file, replacing the file if it already
exists.  data can be a string or a buffer.

If provided, the **chown** option requires both **uid** and **gid** properties or else
you'll get an error.

The **encoding** option is ignored if **data** is a buffer. It defaults to 'utf8'.

Example:

```javascript
writeFileAtomic('message.txt', 'Hello Node', {chown:{uid:100,gid:50}}, function (err) {
  if (err) throw err;
  console.log('It\'s saved!');
});
```

### var writeFileAtomicSync = require('write-file-atomic').sync<br>writeFileAtomicSync(filename, data, [options])

The synchronous version of **writeFileAtomic**.
