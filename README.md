# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. 
STEP-2: Split the plain text into groups of length three. 
STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

char key[]="ABCDEFGHIJKLMNOPQRSTUVWXYZ";
int keymat[3][3]={{1,2,1},{2,3,2},{2,2,1}};
int invkeymat[3][3]={{-1,0,1},{2,-1,0},{-2,2,-1}};

void encodeBlock(char a, char b, char c, char out[4]) {
    int posa=a-'A', posb=b-'A', posc=c-'A';
    int x = (posa*keymat[0][0] + posb*keymat[1][0] + posc*keymat[2][0]);
    int y = (posa*keymat[0][1] + posb*keymat[1][1] + posc*keymat[2][1]);
    int z = (posa*keymat[0][2] + posb*keymat[1][2] + posc*keymat[2][2]);
    
    out[0] = key[(x % 26 + 26) % 26];
    out[1] = key[(y % 26 + 26) % 26]; 
    out[2] = key[(z % 26 + 26) % 26]; 
    out[3] = '\0';
}

void decodeBlock(char a, char b, char c, char out[4]) {
    int posa=a-'A', posb=b-'A', posc=c-'A';
    int x = (posa*invkeymat[0][0] + posb*invkeymat[1][0] + posc*invkeymat[2][0]);
    int y = (posa*invkeymat[0][1] + posb*invkeymat[1][1] + posc*invkeymat[2][1]);
    int z = (posa*invkeymat[0][2] + posb*invkeymat[1][2] + posc*invkeymat[2][2]);
    
    out[0] = key[(x % 26 + 26) % 26]; 
    out[1] = key[(y % 26 + 26) % 26]; 
    out[2] = key[(z % 26 + 26) % 26]; 
    out[3] = '\0';
}

int main() {
    char msg[100] = "Karthic", enc[100] = "", dec[100] = "", block[4];
    
    int originalLen = strlen(msg);

    for(int i=0; msg[i]; i++) msg[i] = toupper(msg[i]);

    int n = strlen(msg) % 3;
    if(n) {
        for(int i = 0; i < 3 - n; i++) {
            strcat(msg, "X");
        }  
    }    

    for(int i = 0; i < strlen(msg); i += 3) { 
        encodeBlock(msg[i], msg[i+1], msg[i+2], block); 
        strcat(enc, block); 
    }

    for(int i = 0; i < strlen(enc); i += 3) { 
        decodeBlock(enc[i], enc[i+1], enc[i+2], block);
        strcat(dec, block);
    }

    dec[originalLen] = '\0';

    printf("Padded: %s\nEncoded: %s\nDecoded (Clean): %s\n", msg, enc, dec);
    return 0;
}
```


## OUTPUT
<img width="252" height="87" alt="image" src="https://github.com/user-attachments/assets/b78f07b8-99f4-4e5f-9988-93896dd4d0e1" />





## RESULT
The code has been executed successfully.
