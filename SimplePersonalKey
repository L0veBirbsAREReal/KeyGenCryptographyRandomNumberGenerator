$OutputDir = "K:\"  # Ensure it's targeting the root of K:

# See readme.md of repository of KeyGenCryptographyRandomNumberGenerator/SimplePersonalKey

# Create the directory if it somehow doesn't exist
if (-not (Test-Path $OutputDir)) {
    New-Item -ItemType Directory -Path $OutputDir -Force | Out-Null
}

function Generate-KeyData {
    $hexValues = @()
    for ($i = 0; $i -lt 8; $i++) {
        $bytes = New-Object byte[] 4
        [System.Security.Cryptography.RandomNumberGenerator]::Create().GetBytes($bytes)
        $value = [BitConverter]::ToUInt32($bytes, 0)
        $hexValues += '{0:X8}' -f $value
    }
    $line1 = ($hexValues[0..3] -join ' ')
    $line2 = "`t`t`t" + ($hexValues[4..7] -join ' ')
    return "$line1`n$line2"
}

function Generate-XMLContent ($Hash, $KeyData) {
    return @"
<?xml version="1.0" encoding="utf-8"?>
<KeyFile>
    <Meta>
        <Version>2.0</Version>
    </Meta>
    <Key>
        <Data Hash="$Hash">
            $KeyData
        </Data>
    </Key>
</KeyFile>
"@
}

for ($i = 1; $i -le 1000000; $i++) {
    $FileName = Join-Path $OutputDir ("keyfile_{0}.keyx" -f $i)
    
    if (Test-Path $FileName) {
        continue  # Skip if file already exists
    }

    $Hash = ([guid]::NewGuid().ToString("N").Substring(0, 8).ToUpper())
    $KeyData = Generate-KeyData
    $Xml = Generate-XMLContent $Hash $KeyData
    Set-Content -Path $FileName -Value $Xml -Encoding UTF8
}

Write-Host "Haystack of 1,000,000 *.keyx files generated in '$OutputDir'"


Write-Host "Light weight, concealable/lo-profile MicroSD key for VeraCrypt, KeePass/XC etc."
Write-Host ""

Write-Host "Perfect, with Kingston USB Micro SD Reader FCR - MRG2 Adapter, I wear it around my neck."
Write-Host "(One in transit, one at A and one at B) I remove to interface via PnP to"
Write-Host "unlock file(s)/containers (eg *.kdbx or VeraCrypt) whether via USB ports on my machine,"
Write-Host "laptop or mobile phone via the now standardised Type-C USB-C OTG Cable Male to USB3."

Write-Host ""

Write-Host "Breaking up the philosophy of security via obscurity,"
Write-Host "a nice addition to following the philosophy of authentication ~ Something You Have,"
Write-Host "Something You Know, and Something You Are..."
Write-Host ""
Write-Host "If the origins of this philosophy do strike intrigue then strike a key when instructed"
Write-Host "Otherwise Ctrl C below as the keys are done. Additionally these type of keys can be"
Write-Host "easily hand written and reconstituted digitally, printed and/or sent under the stamp of"
Write-Host "postage mail. I can't tell you all my tricks but get creative if you are going to post"
Write-Host "a hard drive across Jurisdictions"
Write-Host ""
pause

Start-Process "https://security.stackexchange.com/questions/33667/what-is-the-origin-of-the-three-factors-of-authentication"
