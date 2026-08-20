# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```
#include <stdio.h>

int gcd(int a, int b)
{
    return (b == 0) ? a : gcd(b, a % b);
}

int modExp(int base, int exp, int mod)
{
    int result = 1;

    while (exp > 0)
    {
        if (exp % 2 == 1)
            result = (result * base) % mod;

        base = (base * base) % mod;
        exp = exp / 2;
    }

    return result;
}

int modInv(int a, int m)
{
    int m0 = m;
    int x0 = 0;
    int x1 = 1;

    while (a > 1)
    {
        int q = a / m;
        int t = m;

        m = a % m;
        a = t;

        t = x0;
        x0 = x1 - q * x0;
        x1 = t;
    }

    if (x1 < 0)
        x1 += m0;

    return x1;
}

int main()
{
    int p = 61;
    int q = 53;
    int n = p * q;
    int phi = (p - 1) * (q - 1);
    int e = 17;
    int d;

    char msg[100];
    int encrypted[100];
    int i;

    while (gcd(e, phi) != 1)
        e++;

    d = modInv(e, phi);

    printf("Enter plaintext: ");
    scanf("%s", msg);

    printf("Encrypted: ");

    for (i = 0; msg[i] != '\0'; i++)
    {
        encrypted[i] = modExp(msg[i], e, n);
        printf("%d ", encrypted[i]);
    }

    printf("\nDecrypted: ");

    for (i = 0; msg[i] != '\0'; i++)
    {
        printf("%c", modExp(encrypted[i], d, n));
    }

    printf("\n");

    return 0;
}
```



## Output:
<img width="1052" height="814" alt="CN EX 9" src="https://github.com/user-attachments/assets/46217092-dd75-49e8-b466-b8a8c843a8eb" />



## Result:
 The program is executed successfully.
