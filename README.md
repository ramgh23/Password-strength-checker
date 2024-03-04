import re

class PasswordStrengthChecker:
    def __init__(self, password):
        self.password = password

    def check_length(self):
        return len(self.password) >= 8

    def check_digits(self):
        return bool(re.search(r"\d", self.password))

    def check_uppercase(self):
        return bool(re.search(r"[A-Z]", self.password))

    def check_lowercase(self):
        return bool(re.search(r"[a-z]", self.password))

    def check_special_characters(self):
        return bool(re.search(r"[ !#$%&'()*+,-./[\\\]^_`{|}~" + r'"]', self.password))

    def check_strength(self):
        checks = [
            ('Length', self.check_length()),
            ('Digits', self.check_digits()),
            ('Uppercase', self.check_uppercase()),
            ('Lowercase', self.check_lowercase()),
            ('Special Characters', self.check_special_characters())
        ]
        return [(criteria, passed) for criteria, passed in checks if not passed]

    def get_strength(self):
        failed_checks = self.check_strength()
        if failed_checks:
            return "Weak Password. Missing criteria: {}".format(', '.join([check[0] for check in failed_checks]))
        else:
            return "Strong Password"

# Example usage
password = input("Enter your password: ")
checker = PasswordStrengthChecker(password)
print(checker.get_strength())
