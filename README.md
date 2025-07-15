import random
import time

def spin_slot():
    symbols = ['🍒', '🍋', '🍊', '🍇', '🔔', '7', '💎', '💰']
    
    # Generate three random symbols
    reel1 = random.choice(symbols)
    reel2 = random.choice(symbols)
    reel3 = random.choice(symbols)
    
    # Display spinning animation
    print("\nSpinning...")
    for _ in range(5):
        print(f"\r{random.choice(symbols)} | {random.choice(symbols)} | {random.choice(symbols)}", end="")
        time.sleep(0.1)
    
    # Show final result
    print(f"\r{reel1} | {reel2} | {reel3}", end="")
    
    # Check for wins
    if reel1 == reel2 == reel3:
        print("\n🎉 Jackpot! All three symbols match! 🎉")
        return 10
    elif reel1 == reel2 or reel2 == reel3 or reel1 == reel3:
        print("\n👍 You win! Two symbols match! 👍")
        return 3
    else:
        print("\n😢 No win this time. Try again! 😢")
        return 0

def slot_game():
    credits = 20
    print("Welcome to the Python Slot Machine!")
    print(f"You start with {credits} credits.")
    print("Each spin costs 1 credit. Matching symbols win credits!")
    
    while credits > 0:
        print(f"\nYou have {credits} credits remaining.")
        choice = input("Press Enter to spin or Q to quit: ").upper()
        
        if choice == 'Q':
            break
            
        credits -= 1  # Deduct 1 credit per spin
        winnings = spin_slot()
        credits += winnings
        
    print(f"\nGame over! You finished with {credits} credits.")
    print("Thanks for playing!")

if __name__ == "__main__":
    slot_game()
    
