## TESTING
1. cov1.gft
* Info: The type_of_record statement in examplegiftcardwriter.c was set to 3 in order to communicate with the animate function in giftcardreader.c, which increased coverage.

2. cov2.gft: 
* Info: The gcrd_ptr->type_of_record == 1 statement was changed to gcrd_ptr->type_of_record == 2 in order to increase coverage of cases requiring a value other than 1.

3. fuzzer1.gft
* Info: Using afl-fuzz to create test cases, a hang was revealed in case 0x10 similar to the one in case 0x10.
* Fix: Same as with case 0x09, the issue was fixed by changing the (char)arg1 to (unsigned char)arg1, which disallows negative values. 

4. fuzzer2.gft
* Info: A byte code appeared that was greater than 16, which is the number of available registers in the program. This caused a buffer overflow similar to the one in crash2.gft. 
* Fix: Declare the value of registers as 16 in the animate function, and then validate the arg1 value and ensure it is not greater than 16. If arg1 is found to be greater than 16, the program will terminate with an error.
