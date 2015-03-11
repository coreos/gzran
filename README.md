## gzran
Gzran is a package that reads arbitrary offsets of uncompresssed data from
compressed gzip files. This is accomplished by first inflating a file and
saving decompressor state into memory. Then, the built index can be used with
the `Extract` function to read from the compressed file without fully inflating
the file.

Gzran is based on the c library, zran, by Mark Adler:
https://github.com/madler/zlib/blob/master/examples/zran.c

## example
```go
idx, err := gzran.BuildIndex(gzippedFileName)
if err != nil {
    panic(err)
}
b, err := gzran.Extract(gzippedFileName, idx, fileOffset, readLength)
if err != nil && err != io.EOF {
    panic(err)
}
```
