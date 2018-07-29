## Problem Description:
> Using the credentials from the letter, you logged in to the Foobanizer9000-PC. It has a floppy drive...why? There is an .ico file on the disk, but it doesn't smell right.

1. Extracting the file gives us `foo.ico`
2. Checking the file size using [du](https://linux.die.net/man/1/du) by running `du -h foo.ico` shows that it's a rather large `.ico` file.
3. Therefore, we use [binwalk](https://github.com/ReFirmLabs/binwalk) to analyze the file.
  * `binwalk foo.ico` returns the following.
   
   ```
   DECIMAL       HEXADECIMAL     DESCRIPTION
   --------------------------------------------------------------------------------
   765           0x2FD           Zip archive data, at least v2.0 to extract, compressed size: 123, uncompressed size: 136, name: driver.txt
   956           0x3BC           Zip archive data, at least v2.0 to extract, compressed size: 214, uncompressed size: 225, name: www.com
   1392          0x570           End of Zip archive, footer length: 22
   ```
   
  * There are two zip files of interest. `driver.txt` and `www.com`
4. Running `binwalk -e foo.ico` extracts any recognizable file from `foo.ico`
  * This returns 

### Binwalk is a tool for searching a given binary image for embedded files and executable code. Specifically, it is designed for identifying files and code embedded inside of firmware images.
