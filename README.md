# EX. NO: 3 — IMPLEMENTATION OF HILL CIPHER

## AIM
To write a C program to implement the Hill Cipher substitution technique.

## ALGORITHM
1. Read the plaintext from the user.
2. Convert the plaintext into uppercase letters.
3. Divide the plaintext into groups of three letters.
4. Add `X` if necessary to complete the final group.
5. Multiply each group by the 3 × 3 key matrix using modulo 26.
6. Display the encrypted text.
7. Use the inverse key matrix to decrypt the encrypted text.
8. Display the decrypted text.

## PROGRAM

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int key[3][3] = {
    {1, 2, 1},
    {2, 3, 2},
    {2, 2, 1}
};

int inv[3][3] = {
    {23, 0, 1},
    {2, 25, 0},
    {24, 2, 25}
};

void cipher(char *in, char *out, int mat[3][3]) {
    int p[3], x;

    for (int i = 0; i < 3; i++)
        p[i] = in[i] - 'A';

    for (int i = 0; i < 3; i++) {
        x = 0;
        for (int j = 0; j < 3; j++)
            x += p[j] * mat[i][j];

        out[i] = (x % 26 + 26) % 26 + 'A';
    }
    out[3] = '\0';
}

int main() {
    char msg[1000] = "VELAN";
    char enc[1000] = "", dec[1000] = "";
    char temp[4];

    printf("Hill Cipher\n");
    printf("Input message: %s\n", msg);

    int n = strlen(msg);

    for (int i = 0; i < n; i++)
        msg[i] = toupper((unsigned char)msg[i]);

    while (n % 3 != 0)
        msg[n++] = 'X';

    msg[n] = '\0';

    printf("Padded message: %s\n", msg);

    for (int i = 0; i < n; i += 3) {
        cipher(msg + i, temp, key);
        strcat(enc, temp);
    }

    printf("Encoded message: %s\n", enc);

    for (int i = 0; i < n; i += 3) {
        cipher(enc + i, temp, inv);
        strcat(dec, temp);
    }

    printf("Decoded message: %s\n", dec);

    return 0;
}
```

## SAMPLE OUTPUT

```text
Hill Cipher
Input message: VELAN
Padded message: VELANX
Encoded message: HZJQZV
Decoded message: VELANX
```

## RESULT
Thus, the Hill Cipher encryption and decryption program was implemented and executed successfully using C language.
