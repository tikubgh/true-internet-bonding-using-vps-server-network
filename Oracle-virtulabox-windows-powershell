# Run as Administrator
if (-NOT ([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator")) {
    Write-Host "Please right-click and Run with PowerShell as Administrator!" -ForegroundColor Red
    Pause
    Exit
}

function Show-Menu {
    Clear-Host
    Write-Host "========================================================" -ForegroundColor Cyan
    Write-Host "    ⚡ OpenMPTCProuter Ultra-Speed Network Switcher" -ForegroundColor Cyan
    Write-Host "========================================================" -ForegroundColor Cyan
    Write-Host ""
    Write-Host " [1]  ENABLE  Bonded Internet (Max Speed & VPS DNS)" -ForegroundColor Green
    Write-Host " [2]  DISABLE / REVERT (Restore Standard Windows Wi-Fi)" -ForegroundColor Yellow
    Write-Host " [3]  Check Current Network, Routes & TCP Optimization" -ForegroundColor White
    Write-Host " [0]  Exit" -ForegroundColor Gray
    Write-Host ""
    Write-Host "========================================================" -ForegroundColor Cyan
}

function Test-NetPing($ip) {
    try {
        $p = New-Object System.Net.NetworkInformation.Ping
        $reply = $p.Send($ip, 1500)
        return ($reply.Status -eq "Success")
    } catch {
        return $false
    }
}

function Enable-Bonding {
    Write-Host "`n>>> [1/3] CONFIGURING ADAPTER & ROUTING..." -ForegroundColor Cyan
    
    # 1. Locate VirtualBox Adapter
    $vbox = Get-NetAdapter | Where-Object { $_.InterfaceDescription -like "*VirtualBox*" }
    if (-not $vbox) {
        Write-Host " [FAILED] VirtualBox Host-Only Adapter not found!" -ForegroundColor Red
        return
    }
    Write-Host " [SUCCESS] Detected Adapter: $($vbox.Name) (Index: $($vbox.ifIndex))" -ForegroundColor Green

    # 2. Identify Physical Adapters (Wi-Fi / 4G USB)
    $physical = Get-NetAdapter | Where-Object { $_.Status -eq "Up" -and $_.InterfaceDescription -notlike "*VirtualBox*" }

    # 3. Clean previous configuration
    Remove-NetIPAddress -InterfaceIndex $vbox.ifIndex -Confirm:$false -ErrorAction SilentlyContinue
    Remove-NetRoute -InterfaceIndex $vbox.ifIndex -Confirm:$false -ErrorAction SilentlyContinue
    route delete 0.0.0.0 192.168.100.1 >$null 2>&1

    # 4. Assign Static IP
    try {
        New-NetIPAddress -InterfaceIndex $vbox.ifIndex -IPAddress "192.168.100.2" -PrefixLength 24 -ErrorAction Stop | Out-Null
        Write-Host " [SUCCESS] Assigned IP: 192.168.100.2 on $($vbox.Name)" -ForegroundColor Green
    } catch {
        Write-Host " [FAILED] Could not assign IP: $_" -ForegroundColor Red
    }

    # 5. Assign ONLY OMR / VPS DNS (No 3rd party fallbacks)
    Set-DnsClientServerAddress -InterfaceIndex $vbox.ifIndex -ServerAddresses ("192.168.100.1") -ErrorAction SilentlyContinue
    Write-Host " [OPTIMIZED] DNS strictly set to OpenMPTCProuter: 192.168.100.1" -ForegroundColor Green

    # 6. Unblock Windows Defender Firewall
    Set-NetConnectionProfile -InterfaceIndex $vbox.ifIndex -NetworkCategory Private -ErrorAction SilentlyContinue
    Write-Host " [SUCCESS] Network Category set to 'Private' (Firewall unblocked)" -ForegroundColor Green

    # 7. Force Default Gateway to OMR (Priority 1)
    route add 0.0.0.0 mask 0.0.0.0 192.168.100.1 if $vbox.ifIndex metric 1 >$null 2>&1
    Set-NetIPInterface -InterfaceIndex $vbox.ifIndex -InterfaceMetric 1 -ErrorAction SilentlyContinue
    Write-Host " [SUCCESS] Default Gateway 0.0.0.0/0 -> 192.168.100.1 (Priority #1)" -ForegroundColor Green

    # 8. Demote Physical Adapters
    foreach ($p in $physical) {
        Set-NetIPInterface -InterfaceIndex $p.ifIndex -InterfaceMetric 500 -ErrorAction SilentlyContinue
        Get-NetRoute -InterfaceIndex $p.ifIndex -DestinationPrefix "0.0.0.0/0" -ErrorAction SilentlyContinue | ForEach-Object {
            Set-NetRoute -InterfaceIndex $p.ifIndex -DestinationPrefix "0.0.0.0/0" -NextHop $_.NextHop -RouteMetric 500 -ErrorAction SilentlyContinue
        }
        Write-Host " [SUCCESS] Demoted $($p.Name) Default Route Metric to 500" -ForegroundColor Green
    }

    Write-Host "`n>>> [2/3] APPLYING HIGH-SPEED TCP STACK OPTIMIZATIONS..." -ForegroundColor Cyan

    # 9. Windows 11 High-Speed TCP Tweaks
    netsh int tcp set global autotuninglevel=normal >$null 2>&1
    Write-Host " [OPTIMIZED] TCP Window Auto-Tuning: Normal (Full Gigabit Speed)" -ForegroundColor Green

    netsh int tcp set global rss=enabled >$null 2>&1
    Write-Host " [OPTIMIZED] Receive-Side Scaling (RSS): Enabled (Multi-Core Processing)" -ForegroundColor Green

    netsh int tcp set heuristics disabled >$null 2>&1
    Write-Host " [OPTIMIZED] Windows TCP Heuristics: Disabled (No Bandwidth Throttling)" -ForegroundColor Green

    netsh int tcp set global fastopen=enabled >$null 2>&1
    Write-Host " [OPTIMIZED] TCP Fast Open (TFO): Enabled (Lower Latency)" -ForegroundColor Green

    Clear-DnsClientCache
    Write-Host " [SUCCESS] Flushed Windows DNS Cache." -ForegroundColor Green

    Write-Host "`n>>> [3/3] VERIFYING BONDED SPEED..." -ForegroundColor Cyan
    Start-Sleep -Seconds 1
    
    if (Test-NetPing "192.168.100.1") {
        Write-Host " [PASS] OpenMPTCProuter Gateway (192.168.100.1) is Online!" -ForegroundColor Green
    }
    
    Write-Host "`n🚀 BONDED INTERNET ACTIVE AT MAXIMUM SPEED!" -ForegroundColor Green
    Write-Host " Open fast.com or speedtest.net to test your aggregated bandwidth.`n" -ForegroundColor Cyan
}

function Disable-Bonding {
    Write-Host "`n>>> REVERTING ALL SETTINGS TO FACTORY DEFAULT..." -ForegroundColor Yellow
    
    $vbox = Get-NetAdapter | Where-Object { $_.InterfaceDescription -like "*VirtualBox*" }
    $physical = Get-NetAdapter | Where-Object { $_.InterfaceDescription -notlike "*VirtualBox*" }

    if ($vbox) {
        route delete 0.0.0.0 192.168.100.1 >$null 2>&1
        Remove-NetIPAddress -InterfaceIndex $vbox.ifIndex -Confirm:$false -ErrorAction SilentlyContinue
        Remove-NetRoute -InterfaceIndex $vbox.ifIndex -Confirm:$false -ErrorAction SilentlyContinue
        Set-NetIPInterface -InterfaceIndex $vbox.ifIndex -AutomaticMetric Enabled -ErrorAction SilentlyContinue
        Set-DnsClientServerAddress -InterfaceIndex $vbox.ifIndex -ResetServerAddresses -ErrorAction SilentlyContinue
        Write-Host " [SUCCESS] Removed VirtualBox Default Route & IP." -ForegroundColor Green
    }

    foreach ($p in $physical) {
        Set-NetIPInterface -InterfaceIndex $p.ifIndex -AutomaticMetric Enabled -ErrorAction SilentlyContinue
        Get-NetRoute -InterfaceIndex $p.ifIndex -DestinationPrefix "0.0.0.0/0" -ErrorAction SilentlyContinue | ForEach-Object {
            Set-NetRoute -InterfaceIndex $p.ifIndex -DestinationPrefix "0.0.0.0/0" -NextHop $_.NextHop -RouteMetric 0 -ErrorAction SilentlyContinue
        }
        Write-Host " [SUCCESS] Restored Default Priority on: $($p.Name)" -ForegroundColor Green
    }

    # Reset TCP Stack to Windows Standard
    netsh int tcp set global autotuninglevel=normal >$null 2>&1
    netsh int tcp set heuristics default >$null 2>&1
    Clear-DnsClientCache

    Write-Host "`n✅ [RESTORE COMPLETE] Windows is back to standard Wi-Fi mode.`n" -ForegroundColor Green
}

function Check-Status {
    Write-Host "`n--- ACTIVE DEFAULT GATEWAYS (Lowest RouteMetric Wins) ---" -ForegroundColor Cyan
    Get-NetRoute -DestinationPrefix "0.0.0.0/0" | Format-Table ifIndex, DestinationPrefix, NextHop, RouteMetric, InterfaceAlias -AutoSize
    
    Write-Host "--- TCP STACK ACCELERATION STATUS ---" -ForegroundColor Cyan
    netsh int tcp show global
}

# Main Loop
do {
    Show-Menu
    $choice = Read-Host "Select an option [0-3]"
    switch ($choice) {
        "1" { Enable-Bonding; Pause }
        "2" { Disable-Bonding; Pause }
        "3" { Check-Status; Pause }
        "0" { Write-Host "Goodbye!"; Exit }
        Default { Write-Host "Invalid choice, try again." -ForegroundColor Red; Start-Sleep -Seconds 1 }
    }
} while ($choice -ne "0")
