
# =========================================================
# CODEALPHA PYTHON INTERNSHIP PROJECT
# ALL 4 TASKS IN ONE PROGRAM
# =========================================================

import random
import os
import shutil
import re
import csv

# =========================================================
# MAIN MENU
# =========================================================

def main_menu():
    while True:
        print("\n" + "="*50)
        print("🚀 CODEALPHA PYTHON PROJECT")
        print("="*50)
        print("1. 🎮 Hangman Game")
        print("2. 📈 Stock Portfolio Tracker")
        print("3. ⚙️ Task Automation")
        print("4. 🤖 Basic Chatbot")
        print("5. ❌ Exit")
        
        choice = input("\nEnter your choice: ")

        if choice == "1":
            hangman_game()

        elif choice == "2":
            stock_tracker()

        elif choice == "3":
            automation_task()

        elif choice == "4":
            chatbot()

        elif choice == "5":
            print("\n👋 Thank you for using the project!")
            break

        else:
            print("❌ Invalid choice! Try again.")


# =========================================================
# TASK 1 : HANGMAN GAME
# =========================================================

def hangman_game():
    print("\n🎮 WELCOME TO HANGMAN GAME")

    words = ["python", "computer", "laptop", "developer", "internship"]
    word = random.choice(words)

    guessed_letters = []
    attempts = 6

    while attempts > 0:
        display_word = ""

        for letter in word:
            if letter in guessed_letters:
                display_word += letter + " "
            else:
                display_word += "_ "

        print("\nWord:", display_word)

        if "_" not in display_word:
            print("🎉 Congratulations! You guessed the word.")
            break

        guess = input("Enter a letter: ").lower()

        if guess in guessed_letters:
            print("⚠️ You already guessed that letter.")
            continue

        guessed_letters.append(guess)

        if guess not in word:
            attempts -= 1
            print(f"❌ Wrong guess! Attempts left: {attempts}")

    else:
        print(f"\n💀 Game Over! The word was '{word}'")


# =========================================================
# TASK 2 : STOCK PORTFOLIO TRACKER
# =========================================================

def stock_tracker():
    print("\n📈 STOCK PORTFOLIO TRACKER")

    stock_prices = {
        "AAPL": 180,
        "TSLA": 250,
        "GOOGLE": 150,
        "AMZN": 170,
        "MSFT": 320
    }

    total_value = 0
    portfolio = []

    while True:
        stock = input("\nEnter stock name (or 'done' to finish): ").upper()

        if stock == "DONE":
            break

        if stock not in stock_prices:
            print("❌ Stock not found!")
            continue

        quantity = int(input("Enter quantity: "))

        value = stock_prices[stock] * quantity
        total_value += value

        portfolio.append([stock, quantity, value])

        print(f"✅ Added {stock} worth ${value}")

    print("\n📊 TOTAL INVESTMENT VALUE = $", total_value)

    # Save to CSV
    with open("portfolio.csv", "w", newline="") as file:
        writer = csv.writer(file)

        writer.writerow(["Stock", "Quantity", "Value"])

        for item in portfolio:
            writer.writerow(item)

        writer.writerow(["Total", "", total_value])

    print("💾 Portfolio saved as portfolio.csv")


# =========================================================
# TASK 3 : TASK AUTOMATION
# =========================================================

def automation_task():
    print("\n⚙️ TASK AUTOMATION")

    print("\n1. Move JPG Files")
    print("2. Extract Emails from Text File")

    choice = input("\nEnter your choice: ")

    # OPTION 1 : MOVE JPG FILES
    if choice == "1":

        source_folder = input("Enter source folder path: ")
        destination_folder = input("Enter destination folder path: ")

        if not os.path.exists(destination_folder):
            os.makedirs(destination_folder)

        moved = 0

        for file in os.listdir(source_folder):
            if file.endswith(".jpg"):
                shutil.move(
                    os.path.join(source_folder, file),
                    os.path.join(destination_folder, file)
                )
                moved += 1

        print(f"✅ {moved} JPG files moved successfully!")

    # OPTION 2 : EXTRACT EMAILS
    elif choice == "2":

        filename = input("Enter text file name: ")

        try:
            with open(filename, "r") as file:
                content = file.read()

            emails = re.findall(
                r"[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}",
                content
            )

            with open("emails.txt", "w") as file:
                for email in emails:
                    file.write(email + "\n")

            print("✅ Emails extracted and saved in emails.txt")

        except FileNotFoundError:
            print("❌ File not found!")

    else:
        print("❌ Invalid choice!")


# =========================================================
# TASK 4 : BASIC CHATBOT
# =========================================================

def chatbot():
    print("\n🤖 SIMPLE CHATBOT")
    print("Type 'bye' to exit.\n")

    while True:
        user = input("You: ").lower()

        if user == "hello":
            print("Bot: Hi there! 👋")

        elif user == "how are you":
            print("Bot: I'm fine, thanks! 😊")

        elif user == "what is your name":
            print("Bot: I'm CodeAlpha ChatBot 🤖")

        elif user == "bye":
            print("Bot: Goodbye! 👋")
            break

        else:
            print("Bot: Sorry, I don't understand that.")


# =========================================================
# RUN PROGRAM
# =========================================================

main_menu()


PROJECT SUBMITTED BY
NAGAVENI B KITTUR 
