# Kode standarder for Powershell
Denne kodestandard skal fungere som et grundlag og kan tilpasses efter behov.
Det er vigtigt at opretholde konsistens på tværs af projekter og samarbejde for at sikre en klar og læsbar kode.



## Formatering af Kode
Brug 4 mellemrum for indrykning.
Hold en linje mellem forskellige logiske blokke af kode for bedre læsbarhed.

```PowerShell

function Get-Something {
    # Code here
}

```


## Variable Navngivning
Brug meningsfulde og beskrivende navne til variabler.
Brug camelCase til variabelnavne.

```PowerShell

$computerList
$oldIPAddresses
$userProfileImportPath

```

## Funktioner
Opdel komplekse opgaver i funktioner for at forbedre genbrugelighed og vedligeholdelse.
Nedenstående er et eksempel på en simpel og en advanceret funktion.
Hvis det er en simple funktion, så behøves der ikke alle blokke, "CmdletBinding" eller parametre.

```PowerShell

function Get-Something {
    # Code here
}

```

```PowerShell

function Invoke-SqlStoredProcedure {
    <#
    .SYNOPSIS
        A brief description of the function or script.
    .DESCRIPTION 
        A detailed description of the function or script.
    .PARAMETER SqlPath
        The description of a parameter. Repeat as needed for other parameters.
    .INPUTS
        The types of objects that can be piped to the function or script. You can also include a description of the input objects.
    .OUTPUTS
        The type of the objects that the cmdlet returns. You can also include a description of the returned objects.
    .EXAMPLE
        A sample command that uses the function or script, optionally followed by sample output and a description.
    .NOTES
        Additional information about the function or script.
    #>

    [CmdletBinding()]

    Param(
        [Parameter(Mandatory=$true)][string]$SqlPath,
        [Parameter(Mandatory=$true)][array[]]$ComputerName,
        [Parameter(Mandatory=$false)][int]$UpdateIntervalDays
    )

    begin {
        # Open connections, set variables used in process block ect.
    }

    process {
        # Execute code, write possible return objects ect.
    }

    end {
        # Close connections, release ComObjects, wait for garbage collector ect.
    }
}

```

Se eventuelt nedenstående eller microsofts vejledninger til advancerede funktioner:
https://github.com/PoshCode/PowerShellPracticeAndStyle/blob/master/Style-Guide/Function-Structure.md  
https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-7.4  


### Funktion Navngivning:
Brug verb-noun mønsteret til funktion, såfremt det ikke forværrer forståelsen.
Navngiv funktioner og parametre med PascalCase.

```PowerShell

Get-Process -Name "svchost" -ComputerName "PC0001"
Test-ConnectionMultiThread -Target $addressList
Select-Servers -ComputerName $myServers
Invoke-SqlStoredProcedure -Procedure "insert" -ComputerList $computers

```

Se eventuelt nedenstående og brug gerne "PSScriptAnalyzer" plugin til at hjælpe.  
https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7.4



## Kommentering
Kommenter komplekse dele af koden og vigtige beslutninger. Brug kommentarer til at forklare formålet med funktioner og scripts.
Overvej brugen af "Comment_Based_Help" som vist i tidligere, herved kan "Get-Help" bruges på funktioner.


## Quoting
Brug enkelt anførselstegn for enkle strengværdier, og dobbelt anførselstegn for strengværdier, der kan indeholde variabler.
powershell

```PowerShell

$name = 'John'
$message = "Hello, $name!"

```


## Fejlhåndtering
Implementer try-catch blokke for håndtering af undtagelser.

```PowerShell

try {
    # Kode, der kan forårsage undtagelser
} catch {
    Write-Host "Fejl: $_"
}

```


## Fil Navngivning
Brug meningsfulde og beskrivende navne til filer.  
Scriptfiler: Get-UserData.ps1  
Moduler: MyModule.psm1  
