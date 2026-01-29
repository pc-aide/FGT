# FGT
FGT - Fortigate

````ps1
Add-Type @"
using System;
using System.Runtime.InteropServices;

public class PowerState {
    [DllImport("kernel32.dll", SetLastError = true)]
    public static extern uint SetThreadExecutionState(uint esFlags);

    public const uint ES_CONTINUOUS = 0x80000000;
    public const uint ES_SYSTEM_REQUIRED = 0x00000001;
    public const uint ES_DISPLAY_REQUIRED = 0x00000002;
}
"@

# Active le mode "lecture vidéo"
[PowerState]::SetThreadExecutionState(
    [PowerState]::ES_CONTINUOUS -bor
    [PowerState]::ES_SYSTEM_REQUIRED -bor
    [PowerState]::ES_DISPLAY_REQUIRED
)

Write-Host "🟢 Anti lock actif (Ctrl+C pour arrêter)"

# Boucle silencieuse
while ($true) {
    Start-Sleep -Seconds 60
}

````
