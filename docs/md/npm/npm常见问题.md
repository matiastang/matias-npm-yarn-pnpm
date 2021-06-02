<!--
 * @Author: tangdaoyong
 * @Date: 2021-06-02 11:48:34
 * @LastEditors: tangdaoyong
 * @LastEditTime: 2021-06-02 11:51:41
 * @Description: npm常见问题
-->
# npm常见问题

## Module build failed: Error: ENOENT: no such file or directory

当出现：`Module build failed: Error: ENOENT: no such file or directory`报错时，`unintall`后还是一样的问题，最后按照`Github`上面的的说法：
```
Besides deleting package-lock.json the other workaround here is to upgrade to node-sqlite3@4.0.2
```
把`package-lock.json`删了再执行`npm intall`重新生成`package-lock.json`。