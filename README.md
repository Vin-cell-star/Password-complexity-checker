# Password-complexity-checker
Here's a clean and simple code for a password complexity checker in Python:

```
import re

def check_password_complexity(password):
    """
    Checks the complexity of a password.
    
    Args:
    password (str): The password to check.
    
    Returns:
    dict: A dictionary containing the results of the complexity checks.
    """
    errors = []
    complexity = {
        "length": False,
        "uppercase": False,
        "lowercase": False,
        "digit": False,
        "special_char": False
    }
    
    # Check password length
    if len(password) >= 8:
        complexity["length"] = True
    else:
        errors.append("Password should be at least 8 characters long.")
    
    # Check for uppercase letters
    if re.search(r"[A-Z]", password):
        complexity["uppercase"] = True
    else:
        errors.append("Password should contain at least one uppercase letter.")
    
    # Check for lowercase letters
    if re.search(r"[a-z]", password):
        complexity["lowercase"] = True
    else:
        errors.append("Password should contain at least one lowercase letter.")
    
    # Check for digits
    if re.search(r"\d", password):
        complexity["digit"] = True
    else:
        errors.append("Password should contain at least one digit.")
    
    # Check for special characters
    if re.search(r"[!@#$%^&*(),.?\":{}|<>]", password):
        complexity["special_char"] = True
    else:
        errors.append("Password should contain at least one special character.")
    
    return complexity, errors

def password_strength(complexity):
    """
    Calculates the strength of a password based on its complexity.
    
    Args:
    complexity (dict): A dictionary containing the complexity results.
    
    Returns:
    str: A string describing the password strength.
    """
    score = sum(1 for value in complexity.values() if value)
    
    if score == 5:
        return "Very Strong"
    elif score >= 3:
        return "Strong"
    elif score >= 2:
        return "Medium"
    else:
        return "Weak"

def main():
    password = input("Enter a password: ")
    complexity, errors = check_password_complexity(password)
    strength = password_strength(complexity)
    
    print(f"Password Strength: {strength}")
    print("Complexity:")
    for key, value in complexity.items():
        print(f"{key.capitalize()}: {'OK' if value else 'Not OK'}")
    
    if errors:
        print("\nRecommendations:")
        for error in errors:
            print(error)

if _name_ == "_main_":
    main()
