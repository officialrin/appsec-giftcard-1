## BUGS

1. crash1.gft: null pointer in line 190 of giftcardreader.c
* Info: In examplegiftcardwriter.c, altering the num_bytes from a positive number (116) to a negative one (-116) and compiling it with examplefile.gft will generate .gft file that, when run with the giftcardreader.c program, will cause the program to terminate with a segmentation fault. This is because the negative integer is entered into size_t, which is an unsigned integer, causing it to become a number too large to be stored.
* Fix: Validate the num_bytes value in giftcardreader.c and ensure it is a positive integer. If the num_bytes value is returned as a negative, the program will terminate.

2. crash2.gft: animate function in lines 16 - 67 of giftcardreader.c
* Info:
* Fix:

3. hang.gft: bug to loop program infinitely
* Info:
* Fix: