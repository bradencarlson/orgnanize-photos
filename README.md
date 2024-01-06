# orgnanize-photos
A pair of bash scripts that facilitate sorting many photos into folders by date taken.

## Description
For these scripts to work properly, the `movefiles` and `movemovies` files must be placed in a directory contained in `$PATH`, 
and each of `op`, `om`, `movefiles`, and `movemovies` must be executable. **These scripts may not handle file names 
with spaces correctly, such files will probably not be sorted.**

Once the above conditions are met, place all photos that need to be sorted into a single directory, which is where the scripts 
will create directories and sort the photos.  Once this is done, the program can be called by simply issuing the command 
```
op year1 year2
```
where `year` is the year you wish to begin sorting, and `year2` is the year you wish to end sorting with. For example,
```
op 2016 2023
```
would sort all photos found (of the given filetypes, described below) that were taken between January 1 of 2016 and 
December 31 of 2023, (all photos that have readable metadata that is).  This will be done by creating the directories
```
2016/
2017/
2018/
2019/
2020/
2021/
2022/
2023/
```
one for each year between the years specified by the user, and then creating the directories
```
2016/January/
2016/February/
...
2023/November/
2023/December/
```
The script will then search through photos and, looking at the date the image was taken, move it to the corresponding directory. 
Photos taken outside the provided years will not be moved. Photos with empty or nonreadable metadata will not be moved. 

The om command functions exactly the same, though looks through different filetypes, and uses a different tool to analyze the 
metadata of each file.  This script is much slower (processing about four files per second), but I found that the `exiv2` tool 
used in the op script could not reliably read the metadata on many of the video files I was working with when these files were 
created. 

**The `movefiles` and `movemovies` scripts are not intended to be called by the user.**

## Fine-tuning
To add additional filetypes to either script, simply copy and paste one of the `if..fi` blocks in the `op` or `om` files, and
replace the filetype with the one desired. 
