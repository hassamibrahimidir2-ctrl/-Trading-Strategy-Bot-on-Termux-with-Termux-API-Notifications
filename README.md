README.md (English Version)

# 🤖 Trading Strategy Bot on Termux with Termux API Notifications

A repository designed to run automated Python trading strategies (`python strategy.py live`) on **Termux** for Android devices, featuring instant push notifications powered by **Termux API**.

---

## 📱 Prerequisites
Before getting started, make sure you have installed the following apps from Google Play or F-Droid:
1. **Termux**: Terminal emulator for Android.
2. **Termux-API**: Companion app that allows Termux to control device features (such as sending notifications).

---

## 🛠️ Installation & Setup on Termux

Open your **Termux** app and execute the following commands step by step:

### Step 1: Update system and install essential packages
```bash
pkg update && pkg upgrade -y
pkg install python git termux-api -y

Step 2: Clone the Repository

git clone https://github.com/hassamibrahimidir2-ctrl/My-bot.git
cd My-bot

Step 3: Install required dependencies

pip install --upgrade pip
pip install -r requirements.txt
python strategy.py live

🚀 Usage & Running the Strategy
To run your strategy in Live Trading mode, use the following command

python strategy.py live

🔔 Setting up Termux API Notifications
To enable your bot to send instant push notifications to your phone screen upon executing a trade or triggering an event, use the following Python code snippet:


import subprocess

def send_notification(title, message):
    # Termux API command to send a notification
    cmd = ["termux-notification", "--title", title, "--content", message]
    subprocess.run(cmd)

# Example usage inside your strategy:
# send_notification("Trading Alert 🚨", "Buy order executed successfully!")


⚙️ Running the Bot in the Background (Optional)
If you want the bot to keep running even after closing the Termux app, you can use nohup:

nohup python strategy.py live > bot.log 2>&1 &


To monitor the bot logs:

tail -f bot.log


---

### strategy.py (Example Code)

```python
import sys
import time
import subprocess

def send_notification(title, message):
    try:
        subprocess.run(["termux-notification", "--title", title, "--content", message])
    except Exception as e:
        print(f"Failed to send notification: {e}")

def main():
    mode = sys.argv[1] if len(sys.argv) > 1 else "test"
    print(f"[*] Starting bot in [{mode.upper()}] mode...")
    
    if mode == "live":
        send_notification("Bot Running 🚀", "Trading strategy successfully started on Termux.")
        
        # Dummy loop for strategy execution
        while True:
            print("[*] Checking market conditions...")
            # Place your trading logic here (technical analysis, exchange APIs, etc.)
            
            # Example notification on a specific event:
            # send_notification("New Signal 📈", "Buy opportunity detected at target price.")
            
            time.sleep(60)  # Wait 1 minute before next check
    else:
        print("[-] Please run with 'live' argument: python strategy.py live")

if __name__ == "__main__":
    main()


requirements.txt

requests>=2.28.0






