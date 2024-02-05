# Kode standarder for Powershell
Denne kodestandard skal fungere som et grundlag og kan tilpasses efter behov.
Det er vigtigt at opretholde konsistens på tværs af projekter og samarbejde for at sikre en klar og læsbar kode.



## Formatering af Kode
Brug 4 mellemrum for indrykning.  
Hold en linje mellem forskellige logiske blokke af kode for bedre læsbarhed.  
Fold altid {}-Parenteser ud jo mindre det er reducerer læsbarheden.  

```PowerShell

# Get data - logisk blok 1
function Get-Something {
    # Code here
}

# Use data - logisk blok 2
function Set-Something {
    if ($null -eq $importantStuff) { exit }
    else {
        # Alot of Code here
        # And here
    }
}

```


## Variable Navngivning
Brug meningsfulde og beskrivende navne til variabler.  
Brug PascalCase eller camelCase til variabelnavne.  
Prøv at undlade at bruge forkortelser.  

```PowerShell

$computerList
$oldIPAddresses
$UserProfileImportPath

```

## Funktioner
Opdel komplekse opgaver i funktioner for at forbedre genbrugelighed og vedligeholdelse.  
Simple funktioner behøves ikke alle blokke, "CmdletBinding" eller parametre.  
Nedenstående er et eksempel på en advanceret funktion, overstående ses simple funktioner.  

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
[Function Structure @ PoshCode](https://github.com/PoshCode/PowerShellPracticeAndStyle/blob/master/Style-Guide/Function-Structure.md)  
[About functions @ Microsoft](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-7.4)


### Funktion Navngivning
Brug verb-noun mønsteret til funktion, såfremt det ikke forværrer forståelsen.  
Navngiv funktioner og parametre med PascalCase.  
[Approved verbs for Windows PowerShell @ Microsoft](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7.4)  
[PSScriptAnalyzer @ Microsoft](https://learn.microsoft.com/en-us/powershell/utility-modules/psscriptanalyzer/overview?view=ps-modules)

```PowerShell

Get-Process -Name "svchost" -ComputerName "PC0001"
Test-ConnectionMultiThread -Target $addressList
Select-Servers -ComputerName $myServers
Invoke-SqlStoredProcedure -Procedure "insert" -ComputerList $computers

```



## Kommentering
Kommenter komplekse dele af koden og vigtige beslutninger.  
Overvej brugen af "Comment_Based_Help" som vist i tidligere, herved kan "Get-Help" bruges på funktioner.  
Brug gerne nedenstående template i starten af script.  

```PowerShell

#################################################
# Oprettet af: Anders And
# Oprettet dato: 01.01.2024
# Script til at levere MQ kø-størrelser til CAPMON
# Scriptet er lavet så det kan lægges på alle SPxINTxx servere i prod og preprod
#
# Modificeret af: Peter Belli 25.01.2024
# Tilføjede mulighed for farver. Usage -c
#
# Modificeret af: Anker Petersen 02.02.2024
# Efter mange tests på diverse servere
# så vi at funktionen Trumle altid fejlede på Cisco og derfor
# blev en workaround tilføjet for Cisco. 
#################################################

```

[Comment based help @ Microsoft](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comment_based_help?view=powershell-7.4)  



## Fejlhåndtering
Implementer try-catch blokke for håndtering af undtagelser.

```PowerShell

try {
    # Kode, der kan forårsage undtagelser
} catch {
    Write-Output "Fejl: $_"
    Send-MailMessage -To "vigtigAdmin@regionh.dk" -Body "Fejler med $_" -SmtpServer smtprelay@regionh.top.local
    Write-EventLog -LogName "ICA_Error_Codes" -Source "ICA_Error" -EntryType Error -EventId 1 -Message "$printerName, $server, $name"
    Exit 1
}

```


## Fil Navngivning
Brug meningsfulde og beskrivende navne til filer.  
Hvis filen kun indeholder én funktion så brug eventuelt verb-noun standarden.  
