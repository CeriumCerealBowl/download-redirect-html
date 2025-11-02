Write-Host "=======================================================================================" -ForegroundColor DarkYellow
Write-Host "CeriumNetworks.win Download/Installation Script - Cerium_696" -ForegroundColor Cyan
Write-Host "VERSION 1.1.8 | UPDATED 11/11/25" -ForegroundColor Magenta

# --- CONFIG (Prompt for Drive Letter) ---
Write-Host "💾 Enter the drive letter where the Setup directory should be created (e.g., C, D, E):" -ForegroundColor Cyan
$DriveInput = Read-Host
if (-not $DriveInput) {
    Write-Host "❌ No input provided. Defaulting to C:" -ForegroundColor Yellow
    $Drive = "C:"
} else {
    # Normalize input (add colon if missing)
    if ($DriveInput -notmatch ":$") {
        $Drive = "${DriveInput}:"
    } else {
        $Drive = $DriveInput
    }
}
# --------------------------------------

$BaseDir   = Join-Path $Drive "Setup"
$DepsDir   = Join-Path $BaseDir "Dependencies"
$MsDepsDir = Join-Path $DepsDir "Microsoft"

# Make sure directories exist
$dirs = @($BaseDir, $DepsDir, $MsDepsDir)
foreach ($dir in $dirs) {
    if (-not (Test-Path $dir)) { New-Item -Path $dir -ItemType Directory | Out-Null }
}

# ====================================================================
# Delete old EXE/MSI/ZIP
# ====================================================================
Write-Host "❓ Do you want to delete existing EXE/MSI/ZIP files? (Yes/No)" -ForegroundColor Cyan
$deleteFiles = Read-Host
if ($deleteFiles.ToLower() -eq 'yes') {
    Get-ChildItem -Path $BaseDir, $DepsDir, $MsDepsDir -Include *.exe, *.msi, *.zip -Recurse | Remove-Item -Force
    Write-Host "🗑️ Old installer files deleted." -ForegroundColor Green
} else {
    Write-Host "⏭️ Skipped deleting files." -ForegroundColor Yellow
}

# ====================================================================
# Main Software Downloads
# ====================================================================
$software = @(
    "Google.Chrome",
    "Notepad++.Notepad++",
    "Mozilla.Firefox",
    "OBSProject.OBSStudio",
    "Discord.Discord",
    "Nvidia.GeForceNow",
    "StreetPea.chiaki-ng",
    "Brave.Brave",
    "Google.ChromeRemoteDesktopHost",
    "Valve.Steam",
    "EpicGames.EpicGamesLauncher",
    "7zip.7zip",
    "Parsec.Parsec",
    "Proton.ProtonVPN",
    "Guru3D.Afterburner",
    "Modrinth.ModrinthApp",
    "Audacity.Audacity",
    "Apple.iCloud",
    "Apple.iTunes",
    "RARLab.WinRAR",
    "NordSecurity.NordVPN",
    "RileyTestut.AltServer"
)

$total = $software.Count
for ($i = 0; $i -lt $total; $i++) {
    $id = $software[$i]
    winget download --id=$id -e --accept-package-agreements --accept-source-agreements --download-directory $BaseDir
    Write-Host "✅ Downloaded $id ($($i+1)/$total)" -ForegroundColor Green
}

Write-Host "All main software downloaded to $BaseDir" -ForegroundColor Magenta

# ====================================================================
# Dependencies Downloads
# ====================================================================
$dependencies = @(
    "Microsoft.VCRedist.2013.x86",
    "Microsoft.VCRedist.2013.x64",
    "Microsoft.VCRedist.2010.x64",
    "Microsoft.VCRedist.2005.x86",
    "Microsoft.VCRedist.2008.x86",
    "Microsoft.VCRedist.2008.x64",
    "Microsoft.VCRedist.2005.x64",
    "Microsoft.VCRedist.2015+.x86",
    "Microsoft.VCRedist.2010.x86",
    "Microsoft.VCRedist.2012.x64",
    "Microsoft.VCRedist.2012.x86",
    "Microsoft.VCRedist.2015+.x64",
    "Microsoft.DotNet.DesktopRuntime.7",
    "Microsoft.DotNet.DesktopRuntime.6",
    "Microsoft.DotNet.DesktopRuntime.5",
    "Microsoft.DotNet.DesktopRuntime.3_1",
    "Amazon.Corretto.22.JDK"
)

$depTotal = $dependencies.Count
for ($i = 0; $i -lt $depTotal; $i++) {
    $id = $dependencies[$i]
    $path = if ($id -like "Amazon*") { $DepsDir } else { $MsDepsDir }
    winget download --id=$id --accept-package-agreements --accept-source-agreements --download-directory $path
    Write-Host "✅ Downloaded $id ($($i+1)/$depTotal)" -ForegroundColor Green
}

Write-Host "All dependencies downloaded to $DepsDir and $MsDepsDir" -ForegroundColor Magenta

# ====================================================================
# Delete YAML Files
# ====================================================================
Write-Host "❓ Do you want to delete .yaml files? (Yes/No)" -ForegroundColor Cyan
$deleteYaml = Read-Host
if ($deleteYaml.ToLower() -eq "yes") {
    Remove-Item "$BaseDir\*.yaml","$DepsDir\*.yaml","$MsDepsDir\*.yaml" -Force -ErrorAction SilentlyContinue
    Write-Host "🗑️ All .yaml files removed" -ForegroundColor Green
}

# ====================================================================
# Finish
# ====================================================================
Write-Host "✅ Downloads Complete. Files are in $BaseDir" -ForegroundColor Green
Write-Host "=======================================================================================" -ForegroundColor DarkYellow
Write-Host "CeriumNetworks.win Download/Installation Script - Cerium_696" -ForegroundColor Cyan
Write-Host "VERSION 1.1.8 | UPDATED 11/11/25" -ForegroundColor Magenta