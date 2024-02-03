# Vigenere Cipher Python Project

## Description
A Python program that gives the user the option to encrypt or decrypt a message, or quit the program entirely.
## Code Snippet

```
import time
import sys

print("Jake's Caesar Cipher - Version 1.2")
time.sleep(1)

def get_letters_only_input():
    while True:
        letter_input = input("Please enter the message to encrypt or decrypt. \n")
        if all(char.isalpha() or char.isspace() for char in letter_input):
            if letters_only_confirmation(letter_input):
                time.sleep(1)
                print("Thank you. Moving Ahead.")
                return letter_input
            else:
                time.sleep(1)
                print("Understood. Cancelling Operation. Please enter the plaintext again.")
        else:
            time.sleep(1)
            print("Invalid Input! You must only use letters. \n")

def letters_only_confirmation(user_input):
    while True:
        time.sleep(1)
        user_answer = input(f"Is '{user_input}' what you wanted to use? [Y/N]\n").lower()
        if user_answer == "y":
            return True
        elif user_answer == "n":
            return False
        else:
            time.sleep(1)
            print("Invalid Input! Select [Y/N]")

def get_shift_integer_input():
    while True:
        time.sleep(1)
        try:
            shift_answer = int(input("Please select a number of characters to shift. Your answer can be between 1 and 25.\n"))
            if 1 <= shift_answer <= 25:
                if shift_integer_confirmation(shift_answer):
                    time.sleep(1)
                    print("Thank you. Time to Encrypt/Decrypt. Loading...")
                    return shift_answer
                else:
                    time.sleep(1)
                    print("Understood. Please select an integer between 1 and 25.\n")
            else:
                time.sleep(1)
                print("Invalid Choice! Please select an integer between 1 and 25.\n")
        except ValueError:
            time.sleep(1)
            print("Invalid Input! Please select an integer between 1 and 25.\n")

def shift_integer_confirmation(shift_input):
    while True:
        time.sleep(1)
        shift_input_confirm = input(f"Is '{shift_input}' the number of times you want to shift? [Y/N]\n").lower()
        if shift_input_confirm == "y":
            return True
        elif shift_input_confirm == "n":
            return False
        else:
            time.sleep(1)
            print("Invalid Input! Select [Y/N].")

def encrypt(text, shift):
    result = ""
    for char in text:
        if char.isalpha():
            if char.isupper():
                result += chr((ord(char) + shift - ord('A')) % 26 + ord('A'))
            else:
                result += chr((ord(char) + shift - ord('a')) % 26 + ord('a'))
        else:
            result += char
    return result

def decrypt(text, shift):
    result = ""
    for char in text:
        if char.isalpha():
            if char.isupper():
                result += chr((ord(char) + shift - ord('A')) % 26 + ord('A'))
            else:
                result += chr((ord(char) + shift - ord('a')) % 26 + ord('a'))
        else:
            result += char
    return result

def loading_bar(duration):
    for _ in range(10):
        print("[{}{}]".format("=" * _, " " * (9 - _)), end="\r")
        time.sleep(duration / 10)

def encrypt_or_decrypt():
    while True:
        time.sleep(1)
        option = input("Would you like to [E]ncrypt a message, [D]ecrypt a message, or [Q]uit? [E/D/Q]\n").lower()
        if option == "q":
            time.sleep(1)
            print("Quitting...")
            loading_bar(3)
            sys.exit()
        if option == "e":
            return "encrypt"
        elif option == "d":
            return "decrypt"
        else:
            time.sleep(1)
            print("Invalid Input! Select [E/D]\n")

while True:
    option = encrypt_or_decrypt()

    if option == "encrypt":
        plaintext_string = get_letters_only_input()
        shift_value = get_shift_integer_input()
        encrypted_text = encrypt(plaintext_string, shift_value)

        loading_duration = 5
        loading_bar(loading_duration)
        time.sleep(1)
        print(f"Here is your encrypted message: \n{encrypted_text}")
       
    elif option == "decrypt":
        plaintext_string = get_letters_only_input()
        shift_value = get_shift_integer_input()
        decrypted_text = decrypt(plaintext_string, -shift_value)

        loading_duration = 5
        loading_bar(loading_duration)
        time.sleep(1)
        print(f"Here is your decrypted message: \n{decrypted_text}")
```
