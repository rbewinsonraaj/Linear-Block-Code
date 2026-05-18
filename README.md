# Linear-Block-Code
# Aim
Write a simple python program to Generate Matrix, Codeword, Hamming weight, Syndrome matrix and find the error on received codeword using Linear block code. 
# Tools required
 Google coLab 
# Program
```
]import numpy as np

# Inputs
r = int(input("Enter the Message bits : "))
c = int(input("Enter the Parity bits : "))

# Parity matrix P
P = np.array([list(map(int, input(f"Enter the row values : {i+1} : ").split()))
              for i in range(r)])

# Generator matrix G = [P | I]
I = np.eye(r, dtype=int)
G = np.hstack((P, I))

# All possible message bits
M = np.array([[int(x) for x in format(i, f'0{r}b')] for i in range(2**r)])

# Codewords
C = (M @ G) % 2

# Hamming weights
weights = np.sum(C, axis=1)
dmin = np.min(weights[1:])

# Parity check matrix H = [I | P^T]
H = np.hstack((np.eye(c, dtype=int), P.T))
Ht = H.T

# Output
print('The Generator Matrix is:')
for row in G:
    print(*row)

print('Message Bits  Codeword   Hamming Weight')
for m, cw, w in zip(M, C, weights):
    print(" ".join(map(str,m)), "\t", " ".join(map(str,cw)), "\t", w)

print(f'Minimum Hamming distance : {dmin}')

print('Parity Check Matrix')
for row in H:
    print(*row)

print('Parity Check Matrix Transpose')
for row in Ht:
    print(*row)

# Received codeword
rc = np.array(list(map(int, input("Enter the error codeword : ").split())))

# Syndrome
s = (rc @ Ht) % 2
print("Syndrome of given received codeword is :", *s)

# Error detection
error = np.zeros_like(rc)
for i in range(len(Ht)):
    if np.array_equal(s, Ht[i]):
        error[i] = 1

print("The error position is :", *error)

# Correction
corrected = (rc + error) % 2
print("The correct codeword is :", *corrected)
```
# Output 
![WhatsApp Image 2026-03-13 at 1 37 17 PM](https://github.com/user-attachments/assets/e3e232da-9be0-48e8-9898-3a1947059907)

# Results
Using linear block codes, errors in transmitted data can be efficiently detected and corrected, improving the reliability of communication systems without significantly increasing the data size.
