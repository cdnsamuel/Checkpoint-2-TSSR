# Q2.1
Il faut corriger le chemin
```powershell
Start-Process -FilePath "powershell.exe" -ArgumentList "C:\Scripts\AddLocalUsers.ps1" -Verb RunAs  -WindowStyle Hidden
```
# Q2.2
L44 lors de l'import csv:
- supprimer le flag header car ils sont déjà présents dans le csv
- supprimer le flag skip du select-object
```powershell
$Users = Import-Csv -Path C:\Scripts\Users.csv -Delimiter ";" -Encoding UTF8  | Select-Object
```
# Q2.3
L56 dans l'objet UserInfo ajouter une paire de clé/valeur :
```powershell
$UserInfo = @{
     Name                 = "$Prenom"
     FullName             = "$Prenom.$Nom"
     Description          = "$Description"
     Password             = $Password
     AccountNeverExpires  = $true
     PasswordNeverExpires = $false
}
```
# Q2.4
L44 lors de l'import du csv, ajouter les colonnes à selectionner après select-object :
```powershell
$Users = Import-Csv -Path C:\Scripts\Users.csv -Delimiter ";" -Encoding UTF8  | Select-Object 'prenom','nom','description','fonction'
```
# Q2.5
L67 ajouter en fin de ligne l'affichage du Password
```powershell
Write-Host "L'utilisateur $Prenom.$Nom a été crée avec le mot de passe $Pass"
```
# Q2.6
L68 ajouter une ligne qui appelle la fonction Log :
```powershell
Log -FilePath $LogFile -Content "L'utilisateur $Prenom.$Nom a été crée avec le mot de passe $Pass et la description $Description"
```
# Q2.7
L69 ajouter un bloc else : 
```powershell
    $CheckUserExist = (Get-LocalUser).Name -contains "$Prenom.$Nom"
    If (!$CheckUserExist)
    {
        "..."
    }else{
        Write-Host "L'utilisateur $Prenom.$Nom existe déjà"
        Log -FilePath $LogFile -Content "L'utilisateur $Prenom.$Nom existe déjà "
    }
```
# Q2.8
L67 ajouter un "s" à "Utilisateurs"
```powershell
Add-LocalGroupMember -Group "Utilisateurs" -Member "$Prenom.$Nom"
```
# Q2.9
L50 changer l'attribution
```powershell
$Name = $Prenom,$Nom -join "."
```
L51, 58, 59, 67, 68, 69, 71, 72
remplacer ```$Prenom.$Nom```
par ```$Name```
# Q2.10
L63
```powershell
PasswordNeverExpires = $true
```
# Q2.11
L20
```powershell
Function Random-Password ($length = 10)
```

# Script
```powershell
function Log
{
    param([string]$FilePath,[string]$Content)

    # Vérifie si le fichier existe, sinon le crée
    If (-not (Test-Path -Path $FilePath))
    {
        New-Item -ItemType File -Path $FilePath | Out-Null
    }

    # Construit la ligne de journal
    $Date = Get-Date -Format "dd/MM/yyyy-HH:mm:ss"
    $User = [System.Security.Principal.WindowsIdentity]::GetCurrent().Name
    $logLine = "$Date;$User;$Content"

    # Ajoute la ligne de journal au fichier
    Add-Content -Path $FilePath -Value $logLine
}

Function Random-Password ($length = 10)
{
    $punc = 46..46
    $digits = 48..57
    $letters = 65..90 + 97..122

    $password = get-random -count $length -input ($punc + $digits + $letters) |`
        ForEach -begin { $aa = $null } -process {$aa += [char]$_} -end {$aa}
    Return $password.ToString()
}

Function ManageAccentsAndCapitalLetters
{
    param ([String]$String)
    
    $StringWithoutAccent = $String -replace '[éèêë]', 'e' -replace '[àâä]', 'a' -replace '[îï]', 'i' -replace '[ôö]', 'o' -replace '[ùûü]', 'u'
    $StringWithoutAccentAndCapitalLetters = $StringWithoutAccent.ToLower()
    $StringWithoutAccentAndCapitalLetters
}

$Path = "C:\Scripts"
$CsvFile = "$Path\Users.csv"
$LogFile = "$Path\Log.log"

$Users = Import-Csv -Path $CsvFile -Delimiter ";" -Encoding UTF8  | Select-Object 'prenom','nom','description','fonction'

foreach ($User in $Users)
{
    $Prenom = ManageAccentsAndCapitalLetters -String $User.prenom
    $Nom = ManageAccentsAndCapitalLetters -String $User.nom
    $Name = $Prenom,$Nom -join "."
    $CheckUserExist = (Get-LocalUser).Name -contains "$Name"
    If (!$CheckUserExist)
    {
        $Pass = Random-Password
        $Password = (ConvertTo-secureString $Pass -AsPlainText -Force)
        $Description = "$($user.description) - $($User.fonction)"
        $UserInfo = @{
            Name                 = "$Name"
            FullName             = "$Name"
            Description          = "$Description"
            Password             = $Password
            AccountNeverExpires  = $true
            PasswordNeverExpires = $true
        }

        New-LocalUser @UserInfo
        Add-LocalGroupMember -Group "Utilisateurs" -Member "$Name"
        Write-Host "L'utilisateur $Name a été crée avec le mot de passe $Pass"
        Log -FilePath $LogFile -Content "L'utilisateur $Name a été crée avec le mot de passe $Pass et la description $Description"
    }else{
        Write-Host "L'utilisateur $Name existe déjà"
        Log -FilePath $LogFile -Content "L'utilisateur $Name existe déjà "
    }
}
```