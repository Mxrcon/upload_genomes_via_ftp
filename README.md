# upload_genomes_via_ftp

A python3 program to upload genomes via FTP

# Usage

```bash
> python3 ./upload_liz_genomes.py

```

# Explanation 

1. List of names of genomes to be uploaded

```

genome_list = [
"MTB1.1.fastq.gz",
"MTB8.1.fastq.gz",
"MTB16.1.fastq.gz"
]
```

2. Update the `username` and `password` 

```

ftp = ftplib.FTP("ftp-private.ncbi.nlm.nih.gov", username, password)

```

3. Create a directory using FTP, once you've logged in and you have your own address like `emilyncosta_gmail.com_xxxxx` and create a directory where you'll upload submission `africanum`

```
ftp.cwd("uploads/lizaspinasse_gmail.com_ojGYyyaI")
ftp.mkd("africanum")

```

4. Change the location of the directory 

```
ftp.cwd("uploads/lizaspinasse_gmail.com_ojGYyyaI/WGSMTB")
```

With you information it could be like 

```
ftp.cwd("uploads/emilyncosta_gmail.com_xxxx/africanum")

```


5. The next code is uploading the file one by one 

```python


for a_file in genome_list:
    print("\n@@@@\n\n=> ", a_file,"\n\n@@@")
    with open(a_file ,'rb') as f:
        ftp.storbinary('STOR %s' % f.name , f)


```

6. As a confirmation, after everything is uploaded we confirm from the server 

```

print("\n\n###\n\nList of all Genomes uploaded via FTP:\n\n ")

for f in ftp.nlst():
    print(f)

```

7. We close the FTP connection

```
ftp.quit()

```

8. Now we close the python program

```
print("\n\n$$$\n\nDONE\n\n$$$")
```