# Kode standarder for Bash
Denne kodestandard skal fungere som et grundlag og kan tilpasses efter behov.
Det er vigtigt at opretholde konsistens på tværs af projekter og samarbejde for at sikre en klar og læsbar kode.

## Shebang
Brug altid #!/bin/bash som shebang for at specificere Bash som interpreter.

```Bash

#!/bin/bash

```

## Formatering
Indrykning: Brug fire mellemrum for indrykning.  
Spacing: Brug mellemrum rundt om operatører (=, +, -, *, /) for bedre læsbarhed.

```Bash

if [ "$variable" -eq 0 ]; then
    echo "Success"
else
    echo "Failure"
fi

```

## Navne konventioner
Variable navne: Brug små bogstaver og underscores for at adskille ord (snake_case).  
Konstante navne: Brug store bogstaver og underscores for at adskille ord (SNAKE_CASE).

```Bash

my_variable='value'
MY_CONSTANT='constant_value'

```

## Quotes brug
Brug enkelt citater (' ') for strengkonstanter og dobbelt citater (" ") for variabler eller kommandoer, der skal udvides.

```Bash

message='Hello, World!'
file_path="/path/to/file"
result=$(command)

```

## Kommentering
Brug informative kommentarer for at forklare komplekse dele af koden.
Overvej at bruge # TODO: kommentarer til midlertidige noter.

```Bash

# Dette er en kommentar
if [ "$status" -eq 0 ]; then
    echo "Success"
else
    # TODO: Håndter fejltilstand
    echo "Failure"
fi

```

## Fejlhåndtering:
Brug set -e for at afslutte scriptet ved den første fejl.
Brug trap til at håndtere signaler.

```Bash

Copy code
#!/bin/bash
set -e
trap 'echo "Fejl ved linje $LINENO"; exit 1;' ERR

```

## Brug af funktioner
Brug funktioner til at organisere kode og fremme genbrug.

```Bash

function greet {
    echo "Hello, $1!"
}

greet "World"

```

## Filrettigheder
Sørg for, at scriptet har korrekte filrettigheder for at køre (f.eks. 755).

```Bash

chmod 755 script.sh

```

## Undgå unødig kompleksitet
Hold koden enkel og letforståelig.
Undgå overflødige komplicerede strukturer.

## Skriv portabel kode
Undgå at bruge shell-specifikke funktioner og konstruktioner, der ikke er understøttet på tværs af forskellige systemer.