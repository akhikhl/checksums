#checksums

##Overview

Mass checksum (MD5 and SHA1) calculation for files in the specified folder (recursive to subfolders).

This is gradle script. It is supposed to be run from command line.

To learn what is gradle look here: http://www.gradle.org/

Information on checksum algorithms could be found in many places, for example, here:

http://en.wikipedia.org/wiki/MD5

https://en.wikipedia.org/wiki/Secure_Hash_Algorithm

The script supports two tasks: generateChecksum and cleanChecksum.

##generateChecksums task

###Usage

```shell
gradle -b checksums.gradle
```
or
```shell
gradle generateChecksums -b checksums.gradle
```

###Effect

This task iterates the current folder (where "checksums.gradle" resides) and all it's subfolders,
in each folder it iterates files with extensions "jar", "pom", "xml", for each found file
it calculates MD5-checksum and SHA1-checksum and writes them to .md5 and .sha1 files.

The script accurately calculates inputs/outputs. If all files are supplied with correct checksums,
it does not overwrite any files and shows "UP-TO-DATE" in the console.

###Example

folder and file structure:

<pre>
osgi2maven/1.0.1
osgi2maven/1.0.1/osgi2maven-1.0.1.jar
osgi2maven/1.0.1/osgi2maven-1.0.1.pom
osgi2maven/checksums.gradle
osgi2maven/maven-metadata.xml
</pre>

where "osgi2maven" is current folder, "1.0.1" - it's subfolder.

Running gradle -b checksums.gradle produces the following structure:

<pre>
osgi2maven/1.0.1
osgi2maven/1.0.1/osgi2maven-1.0.1.jar
osgi2maven/1.0.1/osgi2maven-1.0.1.jar.md5
osgi2maven/1.0.1/osgi2maven-1.0.1.jar.sha1
osgi2maven/1.0.1/osgi2maven-1.0.1.pom
osgi2maven/1.0.1/osgi2maven-1.0.1.pom.md5
osgi2maven/1.0.1/osgi2maven-1.0.1.pom.sha1
osgi2maven/checksums.gradle
osgi2maven/maven-metadata.xml
osgi2maven/maven-metadata.xml.md5
osgi2maven/maven-metadata.xml.sha1
</pre>

##cleanChecksums task

###Usage

```shell
gradle cleanChecksums -b checksums.gradle
```

###Effect

Iterates the current folder (where "checksums.gradle" resides) and all it's subfolders,
in each folder it iterates files with extensions "jar", "pom", "xml", for each found file
it removes the corresponding .md5 and .sha1 files.

The script accurately calculates inputs/outputs. If all checksum files were already removed,
it does not remove any files and shows "UP-TO-DATE" in the console.

###Example

folder and file structure:

<pre>
osgi2maven/1.0.1
osgi2maven/1.0.1/osgi2maven-1.0.1.jar
osgi2maven/1.0.1/osgi2maven-1.0.1.jar.md5
osgi2maven/1.0.1/osgi2maven-1.0.1.jar.sha1
osgi2maven/1.0.1/osgi2maven-1.0.1.pom
osgi2maven/1.0.1/osgi2maven-1.0.1.pom.md5
osgi2maven/1.0.1/osgi2maven-1.0.1.pom.sha1
osgi2maven/checksums.gradle
osgi2maven/maven-metadata.xml
osgi2maven/maven-metadata.xml.md5
osgi2maven/maven-metadata.xml.sha1
</pre>

where "osgi2maven" is current folder, "1.0.1" - it's subfolder, 

Running gradle cleanChecksums -b checksums.gradle produces the following structure:

<pre>
osgi2maven/1.0.1
osgi2maven/1.0.1/osgi2maven-1.0.1.jar
osgi2maven/1.0.1/osgi2maven-1.0.1.pom
osgi2maven/checksums.gradle
osgi2maven/maven-metadata.xml
</pre>

##Copyright and License

Copyright 2013 (c) Andrey Hihlovskiy

All versions, present and past, of checksums script are licensed under MIT license:

* [MIT](http://opensource.org/licenses/MIT)
