# Define the testInternetAccess function
function Test-InternetAccess {
    try {
        $response = Invoke-WebRequest -Uri "https://www.google.com" -UseBasicParsing
        if ($response.StatusCode -eq 200) {
            Write-Output "Internet access successful."
        } else {
            Write-Output "Internet access failed."
        }
    } catch {
        Write-Output "Internet access failed."
    }
}

# Define the enableRestrictInternet function
function Enable-RestrictInternet {
    [System.Net.HttpWebRequest]::DefaultWebProxy = New-Object System.Net.WebProxy("http://proxy",$true)
    Write-Output "Internet access restricted."
}

# Define the resetRestrictInternet function
function Reset-RestrictInternet {
    [System.Net.HttpWebRequest]::DefaultWebProxy = $null
    Write-Output "Internet access reset."
}

# Main script
$firstArg = $args[0]

if ($firstArg -eq "testInternetAccess") {
    Test-InternetAccess
} elseif ($firstArg -eq "enableRestrictInternet") {
    Enable-RestrictInternet
} elseif ($firstArg -eq "resetRestrictInternet") {
    Reset-RestrictInternet
} else {
    Write-Output "Usage: defend.ps1 <command>"
    Write-Output "Available commands: testInternetAccess, enableRestrictInternet, resetRestrictInternet"
}

# Clean up your code using PSScriptAnalyzer
# Invoke-ScriptAnalyzer defend.ps1
