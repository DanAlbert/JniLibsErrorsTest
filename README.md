# jniLibs Errors Test

Test case showing bad jniLibs merging.

If two modules provide a native library with the same name, one is
chosen arbitrarily and not even a warning is emitted. Since this cannot be
resolved automatically, this should be an error.

Ignore all the warnings about strip not succeeding. The jniLibs I used
are just text files.

To repro:

```bash
$ cat mylibrary/libs/armeabi-v7a/libfoo.so
0
$ cat app/libs/armeabi-v7a/libfoo.so
1
$ ./gradlew assemble
$ cat \
    app/build/intermediates/merged_jni_libs/release/out/armeabi-v7a/libfoo.so
1
```
