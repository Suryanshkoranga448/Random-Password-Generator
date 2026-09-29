# Random-Password-Generator
A secure, customizable random password generator in Python, available as a library and a command-line tool.
import string
import secrets


def build_character_pool(use_upper, use_lower, use_digits, use_symbols):
    """Create a character pool based on the user's choices."""

    pool = ""

    if use_upper:
        pool += string.ascii_uppercase

    if use_lower:
        pool += string.ascii_lowercase

    if use_digits:
        pool += string.digits

    if use_symbols:
        pool += string.punctuation

    return pool


def generate_password(length, use_upper, use_lower, use_digits, use_symbols):
    """Generate a secure random password."""

    # Create the character pool
    pool = build_character_pool(
        use_upper,
        use_lower,
        use_digits,
        use_symbols
    )

    # Check if at least one character type is selected
    if not pool:
        raise ValueError("Please select at least one character type.")

    # Check password length
    if length < 1:
        raise ValueError("Password length must be at least 1.")

    # Store one character from each selected category
    guaranteed = []

    if use_upper:
        guaranteed.append(
            secrets.choice(string.ascii_uppercase)
        )

    if use_lower:
        guaranteed.append(
            secrets.choice(string.ascii_lowercase)
        )

    if use_digits:
        guaranteed.append(
            secrets.choice(string.digits)
        )

    if use_symbols:
        guaranteed.append(
            secrets.choice(string.punctuation)
        )

    # Check if password is long enough
    if length < len(guaranteed):
        raise ValueError(
            f"Password length must be at least {len(guaranteed)} "
            "for the selected character types."
        )

    # Generate the remaining characters
    remaining_length = length - len(guaranteed)

    for _ in range(remaining_length):
        guaranteed.append(
            secrets.choice(pool)
        )

    # Shuffle all characters
    secrets.SystemRandom().shuffle(guaranteed)

    # Convert list of characters into a string
    return "".join(guaranteed)


def rate_password_strength(password):
    """Return a simple password strength rating."""

    variety = 0

    # Check for uppercase letters
    if any(char.isupper() for char in password):
        variety += 1

    # Check for lowercase letters
    if any(char.islower() for char in password):
        variety += 1

    # Check for numbers
    if any(char.isdigit() for char in password):
        variety += 1

    # Check for special characters
    if any(char in string.punctuation for char in password):
        variety += 1

    # Decide password strength
    if len(password) >= 12 and variety == 4:
        return "Very Strong"

    elif len(password) >= 10 and variety >= 3:
        return "Strong"

    elif len(password) >= 8 and variety >= 2:
        return "Moderate"

    else:
        return "Weak"


def get_yes_no(prompt, default=True):
    """Ask the user a yes/no question."""

    if default:
        options = "[Y/n]"
    else:
        options = "[y/N]"

    while True:
        answer = input(
            f"{prompt} {options}: "
        ).strip().lower()

        # If user presses Enter
        if answer == "":
            return default

        # Yes answers
        if answer in ("y", "yes"):
            return True

        # No answers
        if answer in ("n", "no"):
            return False

        print("Please enter y/yes or n/no.")


def get_positive_integer(prompt, default=None):
    """Get a positive integer from the user."""

    while True:
        answer = input(prompt).strip()

        # Use default value if Enter is pressed
        if answer == "" and default is not None:
            return default

        try:
            number = int(answer)

            if number > 0:
                return number

            print("Please enter a number greater than 0.")

        except ValueError:
            print("Please enter a valid number.")


def main():
    """Run the Random Password Generator."""

    print("=" * 45)
    print("       RANDOM PASSWORD GENERATOR")
    print("=" * 45)

    # Ask for password length
    length = get_positive_integer(
        "Enter desired password length (default 12): ",
        default=12
    )

    print("\nSelect the character types for your password:")

    # Ask which characters should be included
    use_upper = get_yes_no(
        "Include uppercase letters (A-Z)?",
        True
    )

    use_lower = get_yes_no(
        "Include lowercase letters (a-z)?",
        True
    )

    use_digits = get_yes_no(
        "Include digits (0-9)?",
        True
    )

    use_symbols = get_yes_no(
        "Include symbols (!@#$...)?",
        True
    )

    # Check whether at least one type is selected
    if not any([
        use_upper,
        use_lower,
        use_digits,
        use_symbols
    ]):
        print("\nError: Please select at least one character type.")
        print("Program ended.")
        return

    # Count selected character types
    selected_types = sum([
        use_upper,
        use_lower,
        use_digits,
        use_symbols
    ])

    # Check minimum password length
    if length < selected_types:
        print(
            f"\nError: Password length must be at least "
            f"{selected_types} characters."
        )

        print(
            "This is required to include one character "
            "from every selected type."
        )

        return

    # Ask how many passwords to generate
    num_passwords = get_positive_integer(
        "\nHow many passwords do you want to generate? "
        "(default 1): ",
        default=1
    )

    print("\nGenerated Password(s):")
    print("-" * 45)

    # Generate the requested number of passwords
    for i in range(num_passwords):

        password = generate_password(
            length,
            use_upper,
            use_lower,
            use_digits,
            use_symbols
        )

        # Check password strength
        strength = rate_password_strength(password)

        # Display password
        print(
            f"{i + 1}. {password} "
            f"[Strength: {strength}]"
        )

    print("-" * 45)
    print("Password generation completed!")


# Start the program
if __name__ == "__main__":
    main()
