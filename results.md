
# Compression Results

**Notes:**

- **Compression Ratio (CR)** = `Compressed Size / Original Size`
- **Space Savings (SS)** = `1 - Compression Ratio = 1 - (Compressed Size / Original Size)`

## File Comparison

```bash
tar -cf files_archive.tar executable-file.exe image-file.tif large-pdf-file.pdf
xz -z files_archive.tar
```

| File Type  | Original Size (Bytes) | Compressed Size (Bytes) | Compression Ratio (CR) | Space Savings (SS) | Comments                                                                                                                                                                      |
| ---------- | --------------------- | ----------------------- | ---------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Executable | 5,296,128             | 1,510,748               | 29%                    | 71%                | Executable files often contain repetitive binary data, making them reasonably compressible.                                                                                   |
| TIFF Image | 12,603,504            | 798,892                 | 6%                     | 94%                | TIFF uses compression therefore there is not much more that can be compressed.                                                                                                |
| PDF        | 1,081,286             | 864,688                 | 80%                    | 20%                | PDFs can vary in their compressibility depending on their contents. PDFs containing text tend to compress well, but this one contains images or other compressed data do not. |

## Archive Comparisons

```bash
xz -z executable-file.exe image-file.tif large-pdf-file.pdf
tar -cf files_compressed.tar executable-file.exe.xz image-file.tif.xz large-pdf-file.pdf.xz
```

| Archive Type                                | Total Original Size (Bytes) | Total Compressed Size (Bytes) | Compression Ratio (CR) | Space Savings (SS) | Comments |
|---------------------------------------------|-----------------------------|-------------------------------|------------------------|--------------------|----------|
| Tar archive, then xz compress (.tar.xz)     |                             |                               |                        |                    |          |
| Compressed files, then tar archive (.tar)   |                             |                               |                        |                    |          |
| 7zip (LZMA compression, normal level) (.7z) |                             |                               |                        |                    |          |
