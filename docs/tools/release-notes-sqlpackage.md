---
title: Note sulla versione di DacFx e SqlPackage | Microsoft Docs
description: Note sulla versione per sqlpackage Microsoft.
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: 11e10f4a29b15efbd2b0ee513080a2000ae7e2f1
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/29/2019
ms.locfileid: "73033045"
---
# <a name="release-notes-for-sqlpackageexe"></a>Note sulla versione per SqlPackage.exe

**[Scaricare la versione più recente](sqlpackage-download.md)**

Questo articolo elenca le funzionalità e le correzioni distribuite con le versioni rilasciate di SqlPackage.exe.

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="184-sqlpackage"></a>sqlpackage 18.4

|Piattaforma|Scarica|Data di rilascio|Versione|Compilazione
|:---|:---|:---|:---|:---|
|Windows|[Programma di installazione MSI](https://go.microsoft.com/fwlink/?linkid=2108813)|29 ottobre 2019|18.4|15.0.4573.2|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2108815)|29 ottobre 2019| 18,4|15.0.4573.2|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2108814)|29 ottobre 2019| 18.4|15.0.4573.2|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2109019)|29 ottobre 2019| 18.4|15.0.4573.2|

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Distribuzione | Aggiungere il supporto per la distribuzione a Azure SQL Data Warehouse (GA). | 
| Piattaforma | SqlPackage .NET Core GA per macOS, Linux e Windows. | 
| Security | Rimuovere la firma del codice SHA1. |
| Distribuzione | Aggiungere il supporto per le nuove edizioni di database di Azure: GeneralPurpose, BusinessCritical, iperscale |
| Distribuzione | Aggiungere il supporto Istanza gestita per utenti e gruppi di AAD. |
| Distribuzione | Supportare il parametro/AccessToken per SqlPackage in .NET Core. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemi noti 

| Funzionalità | Dettagli |
| :------ | :------ |
| ScriptDom |  Una regressione di analisi di ScriptDom è stata introdotta in 18.3.1, in cui ' RENAME ' viene erroneamente considerato come un token di primo livello, provocando un errore di analisi. Questo problema verrà risolto nella versione successiva di SqlPackage. | 
| &nbsp; | &nbsp; |

### <a name="known-issues-for-net-core"></a>Problemi noti per .NET Core

| Funzionalità | Dettagli |
| :------ | :------ |
| Importa |  Per i file con estensione bacpac con file compressi di dimensioni superiori a 4 GB, potrebbe essere necessario usare la versione .NET Core di SqlPackage per eseguire l'importazione.  Questo comportamento è dovuto al modo in cui .NET Core genera intestazioni zip, che anche se valide, non sono leggibili dalla versione .NET Framework completa di SqlPackage. | 
| Distribuzione | Il parametro/p: Storage = file non è supportato. In .NET Core è supportata solo la memoria. | 
| Always Encrypted | SqlPackage .NET Core non supporta le colonne Always Encrypted. | 
| Security | SqlPackage .NET Core non supporta il parametro/UA per l'autenticazione a più fattori. | 
| Distribuzione | Non sono supportati i file con estensione dacpac e bacpac V2 meno recenti che usano la serializzazione dei dati JSON. |
| &nbsp; | &nbsp; |

## <a name="1831-sqlpackage"></a>sqlpackage 18.3.1

|Piattaforma|Scarica|Data di rilascio|Versione|Compilazione
|:---|:---|:---|:---|:---|
|Windows|[Programma di installazione MSI](https://go.microsoft.com/fwlink/?linkid=2102893)|13 settembre 2019|18.3.1|15.0.4538.1|
|macOS .NET Core (anteprima)|[.zip file](https://go.microsoft.com/fwlink/?linkid=2102894)|13 settembre 2019| 18.3.1|15.0.4538.1|
|Linux .NET Core (anteprima)|[.zip file](https://go.microsoft.com/fwlink/?linkid=2102978)|13 settembre 2019| 18.3.1|15.0.4538.1|
|Windows .NET Core (anteprima)|[.zip file](https://go.microsoft.com/fwlink/?linkid=2102979)|13 settembre 2019| 18.13.1|15.0.4538.1|

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Distribuzione | Aggiungere il supporto per la distribuzione in Azure SQL Data Warehouse (anteprima). | 
| Distribuzione | Aggiungere il parametro/p: DatabaseLockTimeout = (INT32 '60 ') a SqlPackage. | 
| Distribuzione | Aggiungere il parametro/p: LongRunningCommandTimeout = (INT32) a SqlPackage. |
| Esportazione/estrazione | Aggiungere il parametro/p: TempDirectoryForTableData = (STRING) a SqlPackage. |
| Distribuzione | Consente di caricare i collaboratori della distribuzione da percorsi aggiuntivi. I collaboratori alla distribuzione verranno caricati dalla stessa directory di target. dacpac da distribuire, dalla directory Extensions rispetto al file binario SqlPackage. exe e dal parametro/p: AdditionalDeploymentContributorPaths = (STRING) aggiunto a SqlPackage dove è possibile specificare ulteriori percorsi di directory. |
| Distribuzione | Aggiungere il supporto per OPTIMIZE_FOR_SEQUENTIAL_KEY. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Distribuzione | Correzione per ignorare gli indici automatici in modo che non vengano eliminati durante la distribuzione. | 
| Always Encrypted | Correzione per la gestione di Always Encrypted colonne varchar. | 
| Compilazione/Distribuzione | Correzione per risolvere il metodo nodes () per i set di colonne XML.| 
| ScriptDom | Correggere altri casi in cui la stringa ' URL ' è stata interpretata come token di primo livello. | 
| Grafico | Correzione del TSQL generato per i riferimenti pseudo colonna nei vincoli.  | 
| Esportazione | Generare password casuali che soddisfino i requisiti di complessità. | 
| Distribuzione | Correzione per rispettare i timeout dei comandi durante il recupero dei vincoli. | 
| .NET Core (anteprima) | Correzione della registrazione diagnostica in un file. | 
| .NET Core (anteprima) | Usare il flusso per esportare i dati della tabella per supportare tabelle di grandi dimensioni. | 
| &nbsp; | &nbsp; |

## <a name="182-sqlpackage"></a>sqlpackage 18.2

|Piattaforma|Scarica|Data di rilascio|Versione|Compilazione
|:---|:---|:---|:---|:---|
|Windows|[Programma di installazione MSI](https://go.microsoft.com/fwlink/?linkid=2087429)|15 aprile 2019|18.2|15.0.4384.2|
|macOS .NET Core (anteprima)|[.zip file](https://go.microsoft.com/fwlink/?linkid=2087247)|15 aprile 2019 | 18.2 |15.0.4384.2|
|Linux .NET Core (anteprima)|[.zip file](https://go.microsoft.com/fwlink/?linkid=2087431)|15 aprile 2019 | 18.2 |15.0.4384.2|

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Grafico | Aggiunta del supporto di tabelle grafo per i vincoli di arco e le clausole dei vincoli di arco. |
| Distribuzione | Abilitazione della regola di convalida del modello per il supporto di 32 colonne per le chiavi di indice per SQL Server 2016 e versioni successive. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Distribuzione | Correzione del reverse engineering di un database di SQL Server 2016 RTM a causa dell'uso di un hint per la query non supportato. |
| Distribuzione | Correzione dell'ordine di distribuzione in modo che le istruzioni di modifica con chiusura automatica vengano eseguite prima delle istruzioni di creazione di filegroup. |
| ScriptDom | Correzione della regressione di analisi ScriptDom in cui la stringa 'URL' veniva interpretata come un token di primo livello. |
| Distribuzione | Correzione di un'eccezione per riferimento Null durante l'analisi di un'istruzione ALTER TABLE ADD INDEX. | 
| Confronto schema | Correzione del confronto dello schema per le colonne calcolate persistenti che ammettono valori Null che indica sempre differenze.|
| &nbsp; | &nbsp; |

## <a name="181-sqlpackage"></a>sqlpackage 18.1

Data di rilascio: &nbsp; 1 febbraio 2019  
Build: &nbsp; 15.0.4316.1  
Versione di anteprima.

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Distribuzione | Aggiunta del supporto per le regole di confronto UTF8. |
| Distribuzione | Abilitazione degli indici columnstore non cluster su una vista indicizzata. |
| Piattaforma | Passaggio a .NET Core 2.2. | 
| Confronto schema | Uso dell'archiviazione supportata dalla memoria per il confronto schema in .NET Core. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Prestazioni | Correzione delle prestazioni per usare lo strumento di stima della cardinalità legacy per le query di reverse engineering. | 
| Prestazioni | Correzione di un problema di prestazioni significativo di confronto schema durante la generazione di uno script. | 
| Confronto schema | Correzione della logica di rilevamento di deviazione dallo schema per ignorare alcune sessioni di eventi estesi (xevent). |
| Grafico | Correzione dell'ordine di importazione per le tabelle grafo. | 
| Esportazione | Correzione dell'esportazione di tabelle esterne con autorizzazioni per oggetti. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemi noti

Questa versione include le build di anteprima multipiattaforma di sqlpackage destinate a .NET Core 2.2. È supportata l'esecuzione di sqlpackage in macOS e Linux.

| Problema noto | Dettagli |
| :---------- | :------ |
| Distribuzione | Per .NET Core non sono supportati i collaboratori alla compilazione e alla distribuzione. | 
| Distribuzione | Per .NET Core non sono supportati i file con estensione dacpac e bacpac meno recenti che usano la serializzazione dei dati JSON. | 
| Distribuzione | Per .NET Core, possibili errori di risoluzione dei file dacpac (ad esempio master.dacpac) nei riferimenti a causa di problemi con i file system con distinzione tra maiuscole e minuscole. | Una soluzione alternativa consiste nel convertire in maiuscolo il nome del file di riferimento (ad esempio MASTER.BACPAC). |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>sqlpackage 18.0

Data di rilascio: &nbsp; 24 ottobre 2018  
Build: &nbsp; 15.0.4200.1

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Distribuzione | Aggiunta del supporto per il livello di compatibilità del database 150. | 
| Distribuzione | Aggiunta del supporto per le istanze gestite. | 
| Prestazioni | Aggiunta del parametro della riga di comando MaxParallelism per specificare il grado di parallelismo per le operazioni di database. | 
| Security | Aggiunta del parametro della riga di comando AccessToken per specificare un token di autenticazione quando ci si connette a SQL Server. | 
| Importa | Aggiunta del supporto per lo streaming dei tipi di dati BLOB/CLOB per le importazioni. | 
| Distribuzione | Aggiunta del supporto per l'opzione 'INLINE' UDF scalare. | 
| Grafico | Aggiunta del supporto per la sintassi 'MERGE' nella tabella grafo. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Grafico | Correzione della pseudo-colonna non risolta per le tabelle grafo. |
| Distribuzione | Correzione della creazione di un database con filegroup ottimizzati per la memoria quando vengono usate tabelle ottimizzate per la memoria. |
| Distribuzione | Correzione dell'inclusione di proprietà estese per le tabelle esterne. |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>sqlpackage 17.8

Data di rilascio: &nbsp; 22 giugno 2018  
Build: &nbsp; 14.0.4079.2

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Diagnostica | Miglioramento dei messaggi di errore per gli errori di connessione, incluso il messaggio di eccezione SqlClient. |
| Distribuzione | Supporto della compressione dell'indice negli indici a partizione singola per importazione/esportazione. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Distribuzione | Risolto un problema di reverse engineering per set di colonne XML con SQL 2017 e versioni successive. | 
| Distribuzione | Risolto un problema a causa del quale le operazioni di scripting per il livello di compatibilità 140 erano ignorate per il database SQL di Azure. |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>sqlpackage 17.4.1

Data di rilascio: &nbsp; 25 gennaio 2018  
Build: &nbsp; 14.0.3917.1

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Importazione/Esportazione | Aggiunta del parametro della riga di comando ThreadMaxStackSize per analizzare codice Transact-SQL con un numero elevato di istruzioni annidate. |
| Distribuzione | Supporto delle regole di confronto del catalogo di database. | 
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Importa | Sono stati corretti gli errori causati dal _mancato supporto delle chiavi master di database senza password in questa versione di SQL Server_. Tali errori si presentavano al momento dell'importazione di un file con estensione bacpac del database SQL di Azure in un'istanza locale. |
| Grafico | Correzione di un errore di pseudo-colonna non risolta per le tabelle grafo. |
| Confronto schema | Correzione dell'autenticazione SQL per confrontare gli schemi. | 
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>sqlpackage 17.4.0

Data di rilascio: &nbsp; 12 dicembre 2017  
Build: &nbsp; 14.0.3881.1

### <a name="features"></a>Funzionalità

| Funzionalità | Dettagli |
| :------ | :------ |
| Distribuzione |  Aggiunta del supporto per i _criteri di conservazione temporali_ in SQL 2017+ e nel database SQL di Azure. | 
| Diagnostica | Aggiunta del parametro della riga di comando /DiagnosticsFile:"C:\Temp\sqlpackage.log" per specificare un percorso di file per salvare le informazioni di diagnostica. | 
| Diagnostica | Aggiunta del parametro della riga di comando /Diagnostics per registrare le informazioni di diagnostica nella console. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correzioni

| Fix | Dettagli |
| :-- | :------ |
| Distribuzione | Non viene attivato un blocco in presenza di un livello di compatibilità del database non riconosciuto. Viene invece presupposto l'uso della versione più recente del database SQL di Azure o della piattaforma locale. |
| &nbsp; | &nbsp; |
