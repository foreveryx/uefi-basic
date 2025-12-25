# jorge
# UEFI Security Audit Tool

This repository contains a PowerShell utility to collect UEFI-related security posture on Windows devices, including Secure Boot, HVCI/VBS, TPM, and selected firmware context for detecting potential UEFI bypass attempts.

## Usage

### Executar direto do GitHub (PowerShell em qualquer PC)

```powershell
$repoUrl = 'https://raw.githubusercontent.com/foreveryx/uefi-basic/main/UEFISecurityAudit.ps1'
$dest = \"$env:TEMP\\UEFISecurityAudit.ps1\"
Invoke-WebRequest -Uri $repoUrl -OutFile $dest
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
& $dest -OutputPath \"$env:TEMP\\uefi-audit.json\" -IncludeNvramDump -IncludeFirmwareTables
```

- Abra PowerShell como Administrador para melhores resultados; o script também tenta se auto-elevar.  
- O JSON sai em `%TEMP%\uefi-audit.json`.

### Executar localmente (quando já baixado/clonado)

1. Abra PowerShell (Admin é recomendado para acesso a Secure Boot/NVRAM). Se a política bloquear, habilite só na sessão atual:

    ```powershell
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
    ```

2. Rode o script diretamente (o script se auto-eleva se não estiver em Admin):

    ```powershell
    .\scripts\UEFISecurityAudit.ps1 -OutputPath .\uefi-audit.json -IncludeNvramDump -IncludeFirmwareTables
    ```

### Parameters

- `-OutputPath`: Optional path to write a JSON report.
- `-IncludeNvramDump`: Capture additional NVRAM variables (BootOrder, BootNext, BootCurrent, SecureBoot).
- `-IncludeFirmwareTables`: Collect firmware table metadata (ACPI/SMBIOS) for offline review.

The script is read-only and safe to run on production systems. It does not modify firmware or boot entries. Admin rights are recommended to access Secure Boot and firmware interfaces.
