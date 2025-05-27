# Validatore-ICAR-import-2
Strumenti e schemi per validare file in formato XML conformi ai tracciati ICAR Import 2.0


## Utilizzo standard

Per validare un file XML, spostarsi nella directory che contiene "validate.jar" e dare il comando:

```
java -jar validate.jar -v <path-del-file-xml-da-validare> import-2/icar-import.xsd
```

## Utilizzo offline

Per utilizzare il validatore in assenza di collegamento internet - o volendo comunque accelerare l'operazione, evitando lo scaricamento dal web dei vari XML Schema - si può utilizzare gli XML Schema presenti nella directory `import-2-offline`.

Il comando, in tal caso, diventa:

```
java -jar validate.jar -v <path-del-file-xml-da-validare> import-2-offline/icar-import.xsd 
```

## Salvataggio del log in un file di testo

Per salvare l'output della validazione in un file di log, si può usare il seguente comando:

```
java -jar validate.jar -v <path-del-file-xml-da-validare> import-2/icar-import.xsd 1>>"log_%DATE:~6,4%-%DATE:~3,2%-%DATE:~0,2%_%TIME:~0,2%-%TIME:~3,2%.txt" 2>&1
```

Questo comando eseguirà la validazione e salverà l'output in un file di log il cui nome includerà la data e l'ora dell'esecuzione.  
<br>
## Gestione della memoria

Se il file XML da validare è molto grande, potrebbe essere necessario aumentare la memoria disponibile aggiungendo al comando il parametro -Xmx. Questo parametro può essere regolato per aumentare la memoria massima disponibile.

Esempio con 10GB di memoria:

```
java -Xmx10g -jar validate.jar -v <file.xml> import-2/icar-import.xsd
```
Se il validatore restituisce un errore di memoria insufficiente (OutOfMemory), aumentare il valore di -Xmx in base alla RAM disponibile sul proprio sistema.  
<br>
## Validazione multipla con log separato per ogni file

Per validare più file XML presenti nella stessa directory senza la necessità di specificare i nomi e salvare l'output in file di log separati, si può usare il comando:

```
for %f in (*.xml) do java -Xmx6g -jar validate.jar -v "%f" import-2/icar-import.xsd 1>>"log_%~nf_%DATE:~6,4%-%DATE:~3,2%-%DATE:~0,2%_%TIME:~0,2%.txt" 2>&1
```

Il comando eseguirà la validazione su tutti i file XML nella directory e genererà un file di log distinto per ciascun file validato. Il parametro -Xmx è presente e può essere modificato in base alle esigenze. Il nome del file di log includerà il nome del file XML di origine e la data e l'ora dell'esecuzione.
