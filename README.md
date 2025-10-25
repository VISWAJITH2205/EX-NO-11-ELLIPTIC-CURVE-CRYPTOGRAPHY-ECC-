# NAME  : VISWAJITH LALITHRAM R.V

# REG.NO : 212224240187

# EX-NO-11-ELLIPTIC-CURVE-CRYPTOGRAPHY-ECC

## Aim:
To Implement ELLIPTIC CURVE CRYPTOGRAPHY(ECC)


## ALGORITHM:

1. Elliptic Curve Cryptography (ECC) is a public-key cryptography technique based on the algebraic structure of elliptic curves over finite fields.

2. Initialization:
   - Select an elliptic curve equation \( y^2 = x^3 + ax + b \) with parameters \( a \) and \( b \), along with a large prime \( p \) (defining the finite field).
   - Choose a base point \( G \) on the curve, which will be used for generating public keys.

3. Key Generation:
   - Each party selects a private key \( d \) (a random integer).
   - Calculate the public key as \( Q = d \times G \) (using elliptic curve point multiplication).

4. Encryption and Decryption:
   - Encryption: The sender uses the recipient’s public key and the base point \( G \) to encode the message.
   - Decryption: The recipient uses their private key to decode the message and retrieve the original plaintext.

5. Security: ECC’s security relies on the Elliptic Curve Discrete Logarithm Problem (ECDLP), making it highly secure with shorter key lengths compared to traditional methods like RSA.

## Program:
```


#include <stdio.h>

typedef struct { int x, y, inf; } Point;
const int a = 2, b = 3, p = 17;

int mod(int x) { x %= p; return x < 0 ? x + p : x; }

int inv(int k) {
    for (int i = 1; i < p; i++) if (mod(k * i) == 1) return i;
    return -1;
}

Point add(Point P, Point Q) {
    if (P.inf) return Q;
    if (Q.inf) return P;
    Point R = {0, 0, 0};
    int m = (P.x == Q.x && P.y == Q.y)
            ? mod((3 * P.x * P.x + a) * inv(2 * P.y))
            : mod((Q.y - P.y) * inv(Q.x - P.x));
    R.x = mod(m * m - P.x - Q.x);
    R.y = mod(m * (P.x - R.x) - P.y);
    return R;
}

Point mul(Point P, int n) {
    Point R = {0, 0, 1};
    while (n) {
        if (n & 1) R = add(R, P);
        P = add(P, P);
        n >>= 1;
    }
    return R;
}

int main() {
    Point G = {5, 1, 0};
    int n = 7;
    printf("Base point G: (%d, %d)\n", G.x, G.y);
    Point R = mul(G, n);
    if (R.inf) printf("Result of %d * G: Point at Infinity\n", n);
    else printf("Result of %d * G: (%d, %d)\n", n, R.x, R.y);
    printf("=== Code Execution Successful ===\n");
    return 0;
}


```


## Output:


<img width="1135" height="812" alt="11" src="https://github.com/user-attachments/assets/ea8bbe7d-e465-4882-9e6d-7b7b5dbca41f" />



## Result:
The program is executed successfully

