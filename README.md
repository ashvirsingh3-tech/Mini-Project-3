import random
import string

class PasswordError(Exception):
    pass

def generate_password(length=10):
    characters = (
        string.ascii_letters +
        string.digits +
        string.punctuation
    )

    password = "".join(random.choice(characters) for i in range(length))
    return password

def validate_password(password):
    if len(password) < 8:
        raise PasswordError("Password must be at least 8 characters long.")

    if not any(ch.isupper() for ch in password):
        raise PasswordError("Password must contain at least one uppercase letter.")

    if not any(ch.islower() for ch in password):
        raise PasswordError("Password must contain at least one lowercase letter.")

    if not any(ch.isdigit() for ch in password):
        raise PasswordError("Password must contain at least one digit.")

    if not any(ch in string.punctuation for ch in password):
        raise PasswordError("Password must contain at least one special character.")

    print("Password is Strong!")

while True:
    print("\n====== Password Generator & Validator ======")
    print("1. Generate Password")
    print("2. Validate Password")
    print("3. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        length = int(input("Enter Password Length: "))
        print("Generated Password:", generate_password(length))

    elif choice == "2":
        password = input("Enter Password to Validate: ")

        try:
            validate_password(password)
        except PasswordError as e:
            print("Invalid Password:", e)

    elif choice == "3":
        print("Thank You!")
        break

    else:
        print("Invalid Choice! Please try again.")
