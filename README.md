## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




## Program:
import re 
def prepare_text(text): 
text = re.sub(r'[^a-zA-Z]', ', text).lower().replace('j', 'i') 
if len(text) % 2 != 0: 
text += 'z' 
return text 
def create_key_square(key): 
key = '.join(dict.fromkeys(key.replace('j', 'i') + "abcdefghiklmnopqrstuvwxyz")) 
return [list(key[i:i+5]) for i in range(0, 25, 5)] 
def find_positions(key_square, char): 
for i, row in enumerate(key_square): 
if char in row: 
return i, row.index(char) 
def playfair_cipher(text, key, encrypt=True): 
key_square = create_key_square(key) 
text = prepare_text(text) 
result = "" 
shift = 1 if encrypt else -1 
for i in range(0, len(text), 2): 
a, b = text[i], text[i+1] 
r1, c1 = find_positions(key_square, a) 
r2, c2 = find_positions(key_square, b) 
if r1 == r2: 
result += key_square[r1][(c1 + shift) % 5] + key_square[r2][(c2 + shift) % 5] 
elif c1 == c2: 
result += key_square[(r1 + shift) % 5][c1] + key_square[(r2 + shift) % 5][c2] 
else: 
result += key_square[r1][c2] + key_square[r2][c1] 
return result 
def main(): 
4 
key = "suchitra"
plaintext = "saveetha" 
ciphertext = playfair_cipher(plaintext, key, encrypt=True) 
decrypted_text = playfair_cipher(ciphertext, key, encrypt=False) 
print(f"Key: {key}") 
print(f"Plaintext: {plaintext}") 
print(f"Ciphertext: {ciphertext}") 
print(f"Decrypted Text: {decrypted_text}") 
if __name__ == "__main__": 
main()




Output:
![image](https://github.com/user-attachments/assets/086d1337-13e1-478f-8a3a-67e8c03d3964)
