
# Compression ratios and archiving

tar is not a simple command!

## Compression Ratio

Remember that there are two ways to express the compression ratio:

**Compression Ratio (CR)**: This is typically defined as the size of the compressed file divided by the size of the original file:  
$$CR = \frac{\text{compressed size}}{\text{original size}}$$  
A *lower* value means better compression because it indicates a smaller compressed file compared to the original.

**Space Savings (SS)**: The second formula is actually describing the "space savings" or "reduction ratio," which indicates how much space was saved by compression. It's given by:
$$SS = 1 - \frac{\text{compressed size}}{\text{original size}}$$  
This gives a *higher* value for better compression, representing the fraction of space saved (e.g., 0.7 means 70% of the space was saved).

So, the two terms are related but distinct:

- **CR** tells you how much smaller the compressed file is compared to the original (a smaller ratio is better).
- **SS** tells you the percentage of the original file size that was eliminated (a larger percentage is better).

To see the difference, we will compress some files and calculate the ratios.

## **Archiving**

We can have:

- an archive of compressed files
- a compressed archive

We will create both types and see what differences there are.

## Tasks

Use the three test files from Moodle (PDF, executable, and TIFF image). You will need to have the same files available in both Windows and Linux.

Create **THREE** archive files as follows, each containing the three files:

1. On Linux: tar archive of the files, then compress the archive with xz => `.tar.xz` file
2. On Linux: compress the individual files using xz, then put them in a tar archive => `.tar` file
3. On Windows: 7zip archive in a 7z file using normal compression level and LZMA compression => `.7z` file

These should give files with similar compression applied, which we can compare.

### Task A

Using a spreadsheet, record the original and compressed sizes of the files and archives.

### Task B

Calculate the compression ratio for each using BOTH methods in your spreadsheet.

### Task C

Find the difference in size (if any) between the archives in 1, 2, and 3 above. Can you explain this (include answer on the spreadsheet)?

You should start by thinking about your spreadsheet — what information do you need? What are you calculating? How will you lay it out?

Upload your spreadsheet to Moodle. You can use Excel or LibreOffice Calc formats, as you prefer.

**IMPORTANT:** Make sure that your results and answers are clearly presented in the spreadsheet. You will lose marks if they are not.

## **tar options for this assignment**

There are a large number of options for tar, but you only need three for this practical. To add files to an archive using tar, use:

```bash
tar -cvf archive_name.tar list_of_files
```

- The `c` option is "create" to create the archive
- The `v` option is "verbose", which gives you a list of the files as they are added (useful to check it has done what you wanted)
- The `f` option must be followed by the name of the archive you want to create. It's a good idea to call it something.tar so you know what it is afterwards, although tar itself doesn't insist on the name ending in .tar.

### **Compression options**

You won't need many options for the `gzip(1)` and `xz(1)` compression programs. The only useful one is `-k` (for keep). This prevents the compression program from deleting the original uncompressed file once it is finished compressing — the default behavior is to delete the original and replace it with the compressed version (since normally you don't need the uncompressed version anymore).

For example, if you do this:

```bash
xz my_archive.tar
```

You will get a compressed file `my_archive.tar.xz` BUT the original `my_archive.tar` is gone, and you would need to decompress it with `unxz(1)` before continuing, which deletes the compressed file `my_archive.tar.xz`. It's much easier to do this:

```bash
xz -k my_archive.tar
```

Which leaves the `.tar` file as well as the compressed version.

The same `-k` option is available for most other compression programs on Linux.
