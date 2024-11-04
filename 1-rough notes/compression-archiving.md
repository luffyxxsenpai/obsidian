# compression-archiving
---
Date: 03,Oct,2024
subject: compress, decompress, archive in linux 
field: [[linux]]
tags: #tar #zip #unzip #bzip #gzip

---
in windows, we zip unzip some file which relatively decrease the file size saving us some space, now that is done in 2 different process.

1. archiving combines all the files into a large file without reducing any size like a bundle
2. compression reduces the size of that archive by many different methods.

it is important to learn this cause in servers we can have so many old logs or files which we wanna store and it costs money to store or share anything big over internet, so the more efficiently we archive and compress, the more we save money on bandwidth and storage.

## Archive

- tar (tape archive ) is used to handle archives in linux
- tar -c creates a new archive
- tar -x extract files from archive
- tar -t list out the content of a file
- tar -v gives the verbose 
- tar -f for specifying the file, must be used in last
- tar -C extracts to a specific location
- tar -r append files in existing archive
- tar --delete remove file from a uncompressed archive
- tar -exclude to exclude files

- tar -z use gzip compression for `.tar.gz` file
- tar -j use bzip2 compression for `.tar.bz2` file
- tar -J use xz compression for `.tar.xz` file


##### examples
- when you do a operation on a tar file, tarfile name comes first in the command 

1. create a simple tar
	`tar -cf myarchive.tar myfiles`

2. to extract a tar file
	`tar -xf myarchive.tar`
	
3. to see the content of a tar file
	`tar -tf myarchive.tar`

4. to extract to a specific directory
	`tar -xf myarchive.tar -C /home/xyz/`

5. to append a file in a tar file, will add a.txt b.txt abc/
	`tar -rvf myarchive.tar a.txt abc/ b.txt`

6. to delete a file from a tar file, will delete a.txt 
	`tar --delete -f myarchive.tar a.txt`

7. to exclude using a pattern, this will exclude all .txt files from myfiles/testfiles
	`tar -cf myarchive.tar myfiles --exclude='*.txt' myfiles/testfiles/`

8. to exclude specific file
	`tar -cf myarchive.tar myfiles --exclude='myfiles/testfiles/a.txt' --exclude='myfiles/testfiles/b.txt' `


## Compression
- compression reduces the size of files
- linux has gzip, bzip, xz
- we can only compress files instead of directory using these
- we can create a tar file and then use gzip,bzip,xz
- all these 3 will delete original file after compression
- we use `-k` option to keep the original file
- all 3 have similar syntax
- we can use `tar` to directly archive and compress



*size reduction depends on the data, like text based files have high size reduction compared to mp3,jpg,png etc which are already compressed, so we can just archive these files without compressing*

| File Type                                 | **Best Compression**  | **Reason**                                                       |
| ----------------------------------------- | --------------------- | ---------------------------------------------------------------- |
| Text (logs, source code)                  | `gzip`, `bzip2`, `xz` | Text is highly compressible. Choose based on speed vs size.      |
| Already Compressed (images, videos, .zip) | None, just use `tar`  | Already compressed files won't benefit from further compression. |
| Binaries (.exe, .bin)                     | `gzip`, `xz`          | Moderate compression. `xz` for best size, `gzip` for speed.      |
| Large Datasets (CSV, JSON)                | `xz`, `bzip2`         | Best compression for structured, repetitive data.                |
| Mixed File Types                          | `gzip`, `bzip2`       | General-purpose compression for diverse content.                 |
| Large Backups                             | `xz`                  | Best compression ratio for long-term storage of large backups.   |

|             | gzip         | bzip2         | xz         |
| ----------- | ------------ | ------------- | ---------- |
| compress    | gzip -k file | bzip2 -k file | xz -k file |
| decompress  | gzip -d flie | bzip2 -d file | xz -d file |
| tar flag    | -z           | -j            | -J         |
| speed comp  | fast         | moderate      | slow       |
| speed dcomp | very fast    | moderate      | moderate   |


**using tar to compress after making archive**

tar automatically detect the compression type so we dont need to specify any flag while decompressing, but if you want to, you can use z,j,J for gzip,bzip2,xz


1. gunzip
	`tar -czf myarchive.tar.gz myfile`

2. bzip2
	`tar -cjf myarchive.tar.bz2 myfile`

3. xz
	`tar -cJf myarchive.tar.xz myfile`




4. compress using gzip
	`gzip -k hello.tar`

5. decompress using gzip
	`gzip -d hello.tar.gz`

6. compress using bzip2
	`bzip2 -k hello.tar`

7. decompress using bzip2
	`bzip2 -d hello.tar.bz2`

8.  compress using xz
	`xz -k hello.tar`

9. decompress using xz
	`xz -d hello.tar.xz`

---
