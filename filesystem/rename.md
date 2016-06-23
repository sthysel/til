# recursive rename

```
$ find . -name *.txt | xargs rename "s/sums.txt/sums.md5/g"
```

# Perl rename
Match gene indexi and usage of named groups.

```
$ rename 's/([GATC]{8})_([GATC]{8})/$1-$2/g' *
```
