# PowerShell Script to Update Google Chrome using PDQ Deploy

# Define Chrome installer properties
$chromeInstallerUrl = "https://dl.google.com/chrome/install/latest/chrome_installer.exe"
$installerPath = "$env:TEMP\chrome_installer.exe"

# Function to download Chrome installer
function Download-ChromeInstaller {
    Write-Output "Downloading Google Chrome Installer..."
    Invoke-WebRequest -Uri $chromeInstallerUrl -OutFile $installerPath
}

# Function to install Chrome
function Install-Chrome {
    Write-Output "Installing Google Chrome..."
    Start-Process -FilePath $installerPath -Args '/silent /install' -Wait -NoNewWindow
    Remove-Item -Path $installerPath -Force
}

# Check if Chrome is installed & will update
if (Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*' -ErrorAction SilentlyContinue | Where-Object { $_.DisplayName -like '*Google Chrome*' }) {
    Write-Output "Google Chrome is installed. Proceeding with update..."
    Download-ChromeInstaller
    Install-Chrome
    Write-Output "Google Chrome has been updated."
} else {
    Write-Output "Google Chrome is not installed."
}
