# Vigenere Cipher Python Project

## Description
A Python program that gives the user the option to encrypt or decrypt a message, or quit the program entirely. This program utilizes the vigenere cipher.
## Code Snippet

```
# __     ___                                   ____ _       _               
# \ \   / (_) __ _  ___ _ __   ___ _ __ ___   / ___(_)_ __ | |__   ___ _ __ 
#  \ \ / /| |/ _` |/ _ \ '_ \ / _ \ '__/ _ \ | |   | | '_ \| '_ \ / _ \ '__|
#   \ V / | | (_| |  __/ | | |  __/ | |  __/ | |___| | |_) | | | |  __/ |   
#    \_/  |_|\__, |\___|_| |_|\___|_|  \___|  \____|_| .__/|_| |_|\___|_|   
#            |___/                                   |_|                    

#region Import any functions I need here.
import time
#endregion

#region Introduce the user to the program with a friendly message.
print("Jake's Vigenere Cipher")
time.sleep(1)
print("Version 2.4")
time.sleep(1)

#endregion

#region Ask the user for their input string and key for the cipher. We will define these functions to be used later in the program.
def clear_or_encrypted_input():
    while True: #Using a boolean value allows us to verify the integrity of the input text.
        lettter_input = str(input("Please insert the message to be Encrypted or Decrypted. Only letters and spaces are allowed.\n"))
        if all(char.isalpha() or char.isspace() for char in lettter_input):
            time.sleep(1)
            print ("Thank you. Moving Ahead.")
            return lettter_input
        else:
            print ("Invalid input! Please input only letters please.")

def key_input():
    while True: #Using a boolean value allows us to verify the integrity of the input text.
        key_int = str(input("Please input an encryption/decryption key for the cipher. It can be a word or any combination of letters.\n"))
        if all(char.isalpha() for char in key_int):
            time.sleep(1)
            print("Thank you. Moving Ahead.")
            return key_int
        else:
            print ("Invalid input! Please input only letters or words.")
#endregion

#region This will contain the encryption algorithm.
def encrypt(text, key):
    encrypt_text = ""
    key_length = len(key)
    key_space = 0
    for char in text:
        if char.isalpha():
            key_char = key[key_space % key_length]
            shift = ord(key_char.upper()) - ord('A')
            if char.islower():
                encrypt_char = chr((ord(char) - ord('a') + shift) % 26 + ord('a'))
            else:
                encrypt_char = chr((ord(char) - ord('A') + shift) % 26 + ord('A'))
            key_space += 1
        else:
            encrypt_char = char

        encrypt_text += encrypt_char
    return encrypt_text
#endregion

#region This will contain the decryption algorith.
def decrypt(text, key):
    decrypt_text = ""
    key_length = len(key)
    key_space = 0

    for char in text:
        if char.isalpha():
            key_char = key[key_space % key_length]
            shift = ord(key_char.upper()) - ord('A')
            if char.islower():
                decrypt_char = chr((ord(char) - ord('a') - shift + 26) % 26 + ord('a'))
            else:
                decrypt_char = chr((ord(char) - ord('A') - shift + 26) % 26 + ord('A'))
            key_space += 1
        else:
            decrypt_char = char

        decrypt_text += decrypt_char

    return decrypt_text



#endregion

#region Ask the user if they want to encrypt, decrypt, or quit the program. This will be last because I need to define the information gathering and encrytion/decryption functions first.
def choiceMatch():
    while True:
        choice = str(input("Would you like to [E]ncrypt a message, [D]ecrypt a message, or [Q]uit the program? [E/D/N]\n"))
        match choice:
            case "Q":
                print("You chose to Quit the program.")
                time.sleep(1)
                print("Goodbye!")
                break
            case "E":
                time.sleep(1)
                print("You chose to Encrypt a message.")
                plaintextstring = clear_or_encrypted_input()
                key = key_input()
                time.sleep(1)
                print (f"Your encrypted message is: {encrypt(plaintextstring, key)}")
            case "D":
                time.sleep(1)
                print("You chose to decrypt a message.")
                encryptedtextstring = clear_or_encrypted_input()
                key = key_input()
                time.sleep(1)
                print (f"Your decrypted message is: {decrypt(encryptedtextstring, key)}")
            case _:
                print("Invalid Selection! Please select [E/D/Q].")

choiceMatch()
#endregion
```
