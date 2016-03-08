# aws cli 

```
aws --profile=tmeintjes s3 ls --summarize --recursive s3://brl-syd/arundo_donax

aws --profile=tmeintjes s3 --dryrun --recursive mv s3://brl-syd/arundo_donax s3://brl-glacier-syd/1day/arundo_donax/
```
