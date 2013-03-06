Snooker
=======

Snooker is like Pool for sophisticated people.

More rationally, it is a standalone bundling of classes from `android.util.*`
which deal with object pooling.

[![Snooker](snooker.jpg)][2]

*Hat tip to Jeff Gilfelt who [beckons you][3] to use these classes.*



Usage
-----

```java
PoolableManager<Table> tableManager = new PoolableManager<Table>() {
  @Override public Table newInstance() {
    return new SnookerTable(); // Assuming implements/extends Table...
  }

  @Override public void onAcquired(Table table) {
    table.inUse(true);
  }

  @Override public void onReleased(Table table) {
    table.inUse(false);
  }
};
Pool<Table> tables = Pools.finitePool(tableManager, 4);
```

You can now call `tables.acquire()` to obtain a `Table` instance for playing
Snooker. When you are done with your game call `tables.release(table)` which
will return the `table` instance back to the object pool.

For more examples, run `grep -r 'new PoolableManager' .` in the
`frameworks/base/core/java/` folder of AOSP.



Download
--------

Download [the latest JAR][1] or grab via Maven:

```xml
<dependency>
  <groupId>com.jakewharton</groupId>
  <artifactId>snooker</artifactId>
  <version>(insert latest version)</version>
</dependency>
```



License
-------

    Copyright 2009 The Android Open Source Project
    Copyright 2013 Jake Wharton

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.




 [1]: http://repository.sonatype.org/service/local/artifact/maven/redirect?r=central-proxy&g=com.jakewharton&a=snooker&v=LATEST
 [2]: http://www.flickr.com/photos/pikesley/2769018928/
 [3]: https://twitter.com/readyState/status/308649902827786240
