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




Program:
~~~
def generate_key_square(key):
    key = "".join(dict.fromkeys(key.upper().replace("J", "I")))
    alphabet = "ABCDEFGHIKLMNOPQRSTUVWXYZ"
    key += "".join([c for c in alphabet if c not in key])
    return [list(key[i:i+5]) for i in range(0, 25, 5)]

def find_position(square, letter):
    for r, row in enumerate(square):
        if letter in row:
            return r, row.index(letter)

def prepare_text(text):
    text = text.upper().replace("J", "I").replace(" ", "")
    new_text = ""
    i = 0
    while i < len(text):
        a = text[i]
        b = text[i+1] if i+1 < len(text) else "X"
        if a == b:
            new_text += a + "X"
            i += 1
        else:
            new_text += a + b
            i += 2
    return new_text

def playfair(text, key, encrypt=True):
    square = generate_key_square(key)
    text = prepare_text(text)
    result = ""
    for i in range(0, len(text), 2):
        r1, c1 = find_position(square, text[i])
        r2, c2 = find_position(square, text[i+1])
        if r1 == r2:
            result += square[r1][(c1 + (1 if encrypt else -1)) % 5] + square[r2][(c2 + (1 if encrypt else -1)) % 5]
        elif c1 == c2:
            result += square[(r1 + (1 if encrypt else -1)) % 5][c1] + square[(r2 + (1 if encrypt else -1)) % 5][c2]
        else:
            result += square[r1][c2] + square[r2][c1]
    return result

key = "Monarchy"
plaintext = "instruments"
ciphertext = playfair(plaintext, key, True)
decrypted = playfair(ciphertext, key, False)

print("Key:", key)
print("Plaintext:", plaintext)
print("Ciphertext:", ciphertext)
print("Decrypted:", decrypted)
~~~
Output:
Output:
Key text: Monarchy Plain text: instruments Cipher text: gatlmzclrqtx

![Screenshot 2025-03-19 090606](https://github.com/user-attachments/assets/ee615056-c2b8-4693-adce-ec486e699ce9)
## RESULT:
The program is executed successfully


