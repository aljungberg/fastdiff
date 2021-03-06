Compare two folders, fast.

Fastdiff reports blatant differences as quickly as possible, and then finds non-obvious differences given more time. 

If a whole subfolder or file is missing, you'll know within moments. A more subtle difference like a single byte in the beginning of a file you'll know "soon". A very well hidden difference like a byte in a random spot in a huge file, you'll know "eventually".

The longer fastdiff runs, the smaller the chance that any unreported differences remain. This allows a user who is fairly confident that there are no differences to stop the search early. Run fastdiff long enough and it'll do a complete byte for byte comparison.

Some uses:

- Do I need to re-sync this backup copy, is it up to date?
- Is this folder an accidental duplicate of this other folder?
- Has this copy been corrupted (bit rotted) on disk?

Personally I use it to verify my backups.

## Example output

```
$ fastdiff test/a test/b
- Finding files ---------------------------------------------------------------
test/b/a_only.txt missing.
test/a/b_only.txt missing.
test/a/diff_size.txt is 100 bytes but counterpart is 101 bytes (1 byte(s) difference).
test/a/dir_in_1 is a directory but counterpart is not.
test/a/unreadable_a missing.
test/b/recursive/unreadable_b missing.
test/b/recursive_diff/a_only.txt missing.
test/a/recursive_diff/b_only.txt missing.
test/a/recursive_diff/diff_size.txt is 100 bytes but counterpart is 101 bytes (1 byte(s) difference).
test/a/recursive_diff/dir_in_1 is a directory but counterpart is not.
- Quick comparing files -------------------------------------------------------
test/a/diff1.txt and counterpart differ on byte 0.
test/a/diff_last.txt and counterpart differ on byte 18890.
...
test/a/size_8193/diff_on_8191 and counterpart differ on byte 8191.
test/a/size_8193/diff_on_8192 and counterpart differ on byte 8192.
- Fully comparing files (Ctrl-C to cancel) ------------------------------------
test/a/size_32769/diff_on_16384 and counterpart differ on byte 16384.
test/a/size_49152/diff_on_16384 and counterpart differ on byte 16384.
test/a/size_49152/diff_on_16385 and counterpart differ on byte 16385.
test/a/size_49152/diff_on_32767 and counterpart differ on byte 32767.
- Result ----------------------------------------------------------------------
          Total: 90 file pairs (1597695 bytes)
    Fully equal: 5 file pairs (32783 bytes, 2.05%)
Partially equal: 0 file pairs (0 bytes, 0.00%)

      Differing: 85 file pairs (1564912 bytes, 97.95%)
     Unreadable: 0 file pairs (0 bytes, 0.00%)
   Missing left: at least 3 missing file(s) in test/a.
  Missing right: at least 3 missing file(s) in test/b.
```

## Building

```
export GOPATH=$HOME/golang
go get
go build
```

