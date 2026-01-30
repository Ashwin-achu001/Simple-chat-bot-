class Apple:
    def __init__(self):
        self.base_days = 7   # normal apple ripening time
        self.ripening_score = 0

    def simulate_day(self, temperature, ethylene):
        speed = 1

        # temperature effect
        if temperature > 30:
            speed += 0.5
        elif temperature < 15:
            speed -= 0.3

        # ethylene exposure speeds ripening
        if ethylene:
            speed += 0.7

        self.ripening_score += speed

    def stage(self):
        if self.ripening_score >= self.base_days:
            return "Fully Ripe"
        elif self.ripening_score >= self.base_days * 0.6:
            return "Ripe"
        elif self.ripening_score >= self.base_days * 0.3:
            return "Semi-Ripe"
        else:
            return "Raw"


# -------- Program --------

apple = Apple()

days = int(input("Enter number of storage days: "))
temperature = float(input("Enter average temperature: "))
ethylene = input("Ethylene exposure (y/n): ").lower() == 'y'

for _ in range(days):
    apple.simulate_day(temperature, ethylene)

print("\nApple Ripening Status:", apple.stage())
print("Ripening Score:", round(apple.ripening_score, 2))
