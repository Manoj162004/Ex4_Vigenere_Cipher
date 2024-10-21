# Ex4_Vigenere_Cipher

## AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.

## PROGRAM:
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
 
void upper_case(char *src) {
    while (*src != '\0') {
        if (islower(*src))
            *src &= ~0x20;
        src++;
    }
}
 
char* encipher(const char *src, char *key, int is_encode) {
    int i, klen, slen;
    char *dest;
 
    dest = strdup(src);
    upper_case(dest);
    upper_case(key);
 
    /* strip out non-letters */
    for (i = 0, slen = 0; dest[slen] != '\0'; slen++)
        if (isupper(dest[slen]))
            dest[i++] = dest[slen];
 
    dest[slen = i] = '\0'; /* null pad it, make it safe to use */
 
    klen = strlen(key);
    for (i = 0; i < slen; i++) {
        if (!isupper(dest[i]))
            continue;
        dest[i] = 'A' + (is_encode ? dest[i] - 'A' + key[i % klen] - 'A'
                : dest[i] - key[i % klen] + 26) % 26;
    }
 
    return dest;
}
 
int main() {
    const char *str = "Manoj S cse cyber security.Execute Plan B";
    const char *cod, *dec;
    char key[] = "NEVERUSESIMPLEKEY";
 
    printf("Plain Text: %s\n", str);
    printf("key:  %s\n", key);
 
    cod = encipher(str, key, 1);
    printf("cipher text: %s\n", cod);
    dec = encipher(cod, key, 0);
    printf("Decoded text: %s\n", dec);
 
    /* free(dec); free(cod); *//* nah */
    return 0;
}
```
## OUTPUT:
![VigenereCipherOutputImage](Vigenerecipheroutput.png)
## RESULT:
Thus the Vigenere Cipher Encryption and Decrytion using c program successfully implemented .