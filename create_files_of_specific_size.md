Commands to generate files with of specific size. 
This helps you to simulate situations wherever dummy data is required for testing (Log rotation/ Load testing ....)

- **Use dd command**

```
dd if=/dev/zero of=name-of-file  count=N  bs=bytes

Here, 
      bs=BYTES  (read and write BYTES bytes at a time)
      count=N  (copy only N input blocks)
      if=FILE  (read from FILE instead of stdin)
      of=FILE  (write to FILE instead of stdout)
```

Here file of size N*bytes are created with null characters.

- if=/dev/zero  --> creates files with NULL charcters
- if=/dev/urandom --> creates files with random data but not human readable

Examples:
```
To generate 100 MB data:
dd if=/dev/urandom of=file.txt bs=2048 count=10

To generate 1GB data 
dd if=/dev/urandom of=file.txt bs=1048576 count=100
```

- **Use a for loop to copy same data again and again**

```
for i in {1..n}; do cat xxxx.log >> yyyyy.log; done
```
This will generate readable data

- **Use fallocate** 

```
fallocate -l 1G file.txt
```
