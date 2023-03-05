## BUGS

1. crash1.gft: null pointer in line 190 of giftcardreader.c
* Info: In examplegiftcardwriter.c, altering the num_bytes from a positive number (116) to a negative one (-1) and compiling it with examplefile.gft will generate .gft file that, when run with the giftcardreader.c program, will cause the program to terminate with a segmentation fault. This is because the negative integer is entered into size_t, which is an unsigned integer, causing it to become a number too large to be stored.
* Fix: Validate the num_bytes value in giftcardreader.c and ensure it is a positive integer. If the num_bytes value is returned as a negative, the program will terminate with an error.

2. crash2.gft: animate function in lines 16 - 67 of giftcardreader.c
* Info: In giftcardreader.c, we can see in the animate() function that there are 16 registers in the program. We can cause a buffer overflow and trigger a segmentation fault if we make the arg1 value to exceed 16. We can do this by indexing an out of bounds register in case 0x01. changing some values in the giftcardexamplewriter.c program. First, the examplegcrd.record_size_in_bytes must be made negative. Then, the number of bytes can be changed
* Fix: Declare the value of registers as 16, and then validate the arg1 value in giftcardreader.c and ensure it is not greater than 16. If arg1 is found to be greater than 16, the program will terminate with an error.

3. hang.gft: bug to loop program infinitely
* Info: In giftcardreader.c, we can trigger an infinite while loop by passing the value 253(-3) to arg1 in the 0x09 case after changing the examplegcrd.type_of_record value to 3. This is because the original argument causes the pointer to move forward 3 memory location, so if the 0x09 case is changed to move the pointer backwards 3, it will infinitely loop back and forth.
* Fix: The (char)arg1 in case 0x09 can be changed to (unsigned char)arg1 which will disallow it from accepting a negative value, thus fixing the infinite loop issue.