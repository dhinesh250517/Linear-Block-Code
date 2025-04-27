# LINEAR BLOCK CODE
## AIM :
To Perform linear Block code operation for the given input

## TOOLS REQUIRED :
Python IDE with Numpy and Scipy

## PROGRAM:
```
import numpy as np
pb = [] # Parity matrix
Ik = [] # I_K Matrix
p = []
m = []
h = []
h_dis = []
r_code = []
err = []
col = int(input("Enter the Parity bits : "))
row = int(input("Enter the Message bits : "))
# Generator matrix
for i in range (row):
  p = list(map(int, input(f"Enter the row values : {i+1} (Separated by space) : ").split()))
  pb.append(p)
p_mat = np.array(pb, dtype=int)
Ik=np.eye(row, dtype=int) # Diagonal Matrix
g_mat = np.hstack((p_mat,Ik)) # Generator Matris

# Codeword length and parity bit length
n, k = g_mat.T.shape
# Possible Message Bits
m = np.array([[1 if (i >> (k - j - 1)) & 1 else 0 for j in range(k)] for i in range(2**k)])
# Codewords and Hamming weights
c = np.mod(np.dot(m, g_mat), 2)
for i, row in enumerate(c):
  h_dis1 = np.sum(row) # Count number of 1's in the row
  h_dis.append(h_dis1)
h_mat = np.array(h_dis).reshape(1,-1)
#h_mat = np.hstack(h_mat)
d_min = np.min(np.sum(c[1:], axis=1))
# H matrix (Parity-check matrix)
h = p_mat[:, :3]
hp = np.hstack((np.eye(n-k, dtype=int), h.T))
ht = hp.T
print('')
print('The Generator Matrix is: ')
#for r in p_mat: 
#    print(" ".join(map(str, r)))
#for r in Ik: 
#    print(" ".join(map(str, r)))
for r in g_mat: 
  print(" ".join(map(str, r)))
print('')
print(f'Message Bits      Codeword     Hamming Weight')
code_word = np.hstack((m, c, h_mat.T))
for r in range(code_word.shape[0]):
  format_row = " ".join(map(str, code_word[r, :k])) + '\t\t' + " ".join(map(str, code_word[r, k:n+k])) + '\t\t' + str(code_word[r, -1])
  print(format_row)
print('')
print(f'Minimum Hamming distance : {d_min}')
# Parity Check matrix
print('')
print(f'Parity Check Matrix')
for r in hp:
  print(" ".join(map(str, r)))
print('')
print(f'Parity Check Matrix Transpose')
for r in ht:
  print(" ".join(map(str, r)))
#Receive codeword
rc = list(map(int, input(f"Enter the error codeword : ").split()))
r_code.append(rc)
r_c = np.array(r_code)
#Syndrome Calculation
e = np.mod(np.dot(r_c, ht), 2)

#print('')
#print(f'Received codeword Matrix')
#for r in r_c:
#    print(" ".join(map(str, r)))
print('')
print(f"Syndeome of given received codeword is : " + " ".join(map(str, e[0])))
print('')
print(f'Syndrome Matrix')
for i in range(n):
  combined_row = np.concatenate((ht[i, :], np.eye(n, dtype=int)[i,:]))
  formatted_row = " ".join(map(str, combined_row[:3])) + '\t' + " ".join(map(str, combined_row[k:]))
  print(f'{formatted_row}')
# Find the Error position
for i in range(n):
  if np.array_equal(e[0], ht[i, :]):
    err = np.eye(n, dtype=int)[i,:]
print(f"The error postion is : " + " ".join(map(str, err)))
# Correct the error in the received codeword
add = err + rc
print(f"The correct codeword is : " + " " .join(map(str,add)))
```
## OUTPUT:

![image](https://github.com/user-attachments/assets/a07b421c-cfca-4539-a46e-2c1744652793)
![image](https://github.com/user-attachments/assets/9dd376f7-ecd3-4183-985e-34a066e9a057)



## CALCULATION
![WhatsApp Image 2025-04-27 at 13 34 59_71d3c2a4](https://github.com/user-attachments/assets/3c973200-014d-4661-bd6a-25bb55ba826c)
![WhatsApp Image 2025-04-27 at 13 34 59_fc50195f](https://github.com/user-attachments/assets/147caf98-6f75-4983-874c-fcc4998584cb)
![WhatsApp Image 2025-04-27 at 13 35 11_c5758f38](https://github.com/user-attachments/assets/dca021fc-da82-4c00-9e6d-686bb2ac968e)





## RESULTS:
Thus,Linear Block Code for the Given input is successfully verified
