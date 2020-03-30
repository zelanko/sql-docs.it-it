---
title: Domande frequenti
titleSuffix: Azure Data Studio
description: Domande frequenti su Azure Data Studio.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 1916a10a468fdc44c021e410eb1521cb7c219d58
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67959543"
---
# <a name="azure-data-studio-faq"></a>Domande frequenti su [!INCLUDE[Azure Data Studio](../includes/name-sos.md)]

## <a name="what-is-azure-data-studio"></a>Che cos'è Azure Data Studio?

Azure Data Studio è un nuovo ambiente desktop multipiattaforma open source per professionisti della gestione dei dati che usano la famiglia Azure di piattaforme dati locali e cloud in Windows, MacOS e Linux. Precedentemente rilasciato con il nome di anteprima di SQL Operations Studio, Azure Data Studio offre un'esperienza di modifica moderna per la gestione dei dati tra più origini con funzionalità IntelliSense veloce, frammenti di codice, integrazione del controllo del codice sorgente e un terminale integrato. Azure Data Studio è stato progettato in base alle esigenze dell'utente della piattaforma dati, con grafici predefiniti di set di risultati delle query e dashboard personalizzabili.

La ricerca ha dimostrato che gli utenti dedicano alla modifica delle query molto più tempo rispetto a qualsiasi altra attività con SQL Server Management Studio. Per questo motivo, Azure Data Studio è stato progettato con una particolare attenzione alle funzionalità più usate, con esperienze aggiuntive disponibili come estensioni facoltative del prodotto. In questo modo, ogni utente può personalizzare il proprio ambiente per i flussi di lavoro che usa più spesso.


## <a name="how-much-does-azure-data-studio-cost"></a>Quanto costa Azure Data Studio?

Azure Data Studio è gratuito per uso privato o commerciale.

## <a name="who-should-use-azure-data-studio"></a>Chi dovrebbe usare Azure Data Studio?

Chiunque può usare Azure Data Studio. Tuttavia, è progettato per semplificare le attività eseguite da sviluppatori di database, amministratori di database, amministratori di sistema e fornitori di software indipendenti.

## <a name="what-can-i-do-with-azure-data-studio"></a>Cosa si può fare con Azure Data Studio?

Azure Data Studio è basato su Visual Studio Code e offre un'esperienza di codifica leggera, moderna e incentrata sulla tastiera quando si usano SQL Server, il database SQL di Azure o Azure SQL DW. Azure Data Studio semplifica le attività quotidiane grazie a funzionalità integrate quali finestre a più schede, un editor SQL avanzato, IntelliSense, completamento delle parole chiave, frammenti di codice, esplorazione del codice e integrazione del controllo del codice sorgente (Git e TFS). È possibile eseguire query su richiesta, visualizzare e salvare i risultati in formato testo, JSON o Excel, modificare i dati, organizzare e gestire le connessioni di database preferite e sfogliare gli oggetti di database in un'esperienza di esplorazione familiare.

Nella finestra del terminale integrato all'interno dell'interfaccia utente di Azure Data Studio si possono usare i propri strumenti da riga di comando preferiti, ad esempio Bash, PowerShell, sqlcmd, bcp, psql e ssh. È semplice generare ed eseguire script di creazione e inserimento per gli oggetti di database, per creare copie del database a scopo di sviluppo o test. I frammenti di codice intelligenti e le ricche esperienze grafiche per creare nuovi database e oggetti di database (come tabelle, viste, stored procedure, utenti, accessi, ruoli e così via), nonché aggiornare gli oggetti di database esistenti, aumentano la produttività. È possibile usare dashboard avanzati e personalizzabili per monitorare e risolvere rapidamente i colli di bottiglia delle prestazioni nei database in locale, in Azure o in qualunque cloud.

Azure Data Studio offre un'esperienza coerente per eseguire il backup e il ripristino dei database. Grazie al supporto pianificato per i gruppi di disponibilità Always On di SQL Server, è possibile configurare, monitorare e risolvere facilmente i problemi relativi ai gruppi di disponibilità per i database di SQL Server cruciali ed eseguire rapidamente il failover in un database secondario durante un'emergenza. Azure Data Studio è stato progettato per migliorare la produttività nel ciclo di vita DevOps per i database e nei sistemi operativi scelti dagli utenti. Di conseguenza, si ha sempre il pieno controllo ed è possibile ridurre i rischi, risolvere i problemi più rapidamente e fornire continuamente un valore che supera le aspettative dei clienti.

## <a name="is-azure-data-studio-open-source"></a>Azure Data Studio è open source?

Il codice sorgente per Azure Data Studio e per i suoi provider di dati è disponibile su GitHub. Il codice sorgente per il front-end Azure Data Studio (basato su Visual Studio Code) è disponibile in base a un contratto di licenza che fornisce il diritto di modificare e usare il software, ma non di ridistribuirlo o ospitarlo in un servizio cloud. Il codice sorgente per i provider di dati è disponibile in base ai termini della licenza MIT all'indirizzo [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-we-plan-to-open-source-ssms"></a>SQL Server Management Studio verrà reso open source?

No. Tuttavia, gli strumenti CLI e GUI di nuova generazione per più sistemi operativi sono open source. Ad esempio, l'estensione mssql per VS Code, mssql-scripter, e msql-CLI sono tutti open source su GitHub. Il codice sorgente di Azure Data Studio è disponibile su GitHub.  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>Ora che esiste Azure Data Studio, Microsoft prevede di deprecare SSMS e SSDT? 

No. Gli investimenti negli strumenti principali di Windows (SSMS, SSDT, PowerShell) proseguiranno di pari passo con la nuova generazione di strumenti CLI e GUI multi-database e multi-sistema operativo. L'obiettivo è offrire ai clienti la possibilità di scegliere di usare gli strumenti che preferiscono, sulle piattaforme più idonee per i propri scenari. Azure Data Studio è maggiormente incentrato sulle esperienze di modifica delle query e sviluppo dati, che secondo la ricerca è la capacità di gran lunga più usata in SQL Server Management Studio. Come estensioni di Azure Data Studio sono anche disponibili altre funzionalità amministrative di valore elevato, ad esempio backup, ripristino, gestione dei processi agente e profilatura dei server. Azure Data Studio è multipiattaforma, per cui consente agli utenti di lavorare sulla propria piattaforma preferita. SQL Server Management Studio, tuttavia, offre ancora la più ampia gamma di funzioni amministrative e rimane lo strumento di punta per le attività di gestione della piattaforma. 

## <a name="when-should-i-use-azure-data-studio-vs-sql-server-management-studio"></a>Quando è consigliabile usare Azure Data Studio anziché SQL Server Management Studio?

*Usare Azure Data Studio se:*

- Si dedica la maggior parte del tempo alla modifica o all'esecuzione di query.
- È necessario poter creare rapidamente grafici e visualizzare set di risultati.
- Si può eseguire la maggior parte delle attività amministrative tramite il terminale integrato usando sqlcmd o PowerShell.
- Si ha una necessità minima di esperienze di tipo procedura guidata.
- Non è necessario eseguire operazioni approfondite di configurazione amministrativa o della piattaforma.
- L'ambiente di esecuzione è macOS o Linux.

*Usare SQL Server Management Studio se:*

- Si dedica la maggior parte del tempo ad attività di amministrazione di database.
- Si eseguono operazioni approfondite di configurazione amministrativa o della piattaforma.
- Ci si occupa di gestione della sicurezza, incluse gestione degli utenti, valutazione della vulnerabilità e configurazione delle funzionalità di sicurezza.
- È necessario usare dashboard e procedure guidate di ottimizzazione delle prestazioni.
- Si usano diagrammi di database e progettazione tabelle.
- Si esegue l'importazione/esportazione di file DACPAC.
- È necessario accedere ai server registrati.
- Si usano la modalità sqlcmd, statistiche sulle query dinamiche o statistiche client.

## <a name="feature-comparison"></a>Confronto tra le funzionalità

### <a name="shell-features"></a>Funzionalità shell

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Accesso ad Azure|Sì|Sì|
|Dashboard|Sì| |
|Estensioni|Sì| |
|Terminale integrato|Sì||
|Esplora oggetti|Sì|Sì|
|Scripting per gli oggetti|Sì|Sì|
|Sistema di progetto|Sì||
|Selezione da tabella|Sì|Sì|
|Controllo del codice sorgente|Sì||
|Riquadro attività|Sì||
|Temi|Sì||
|Modalità scura|Sì||
|Azure Resource Explorer|Anteprima||
|Procedura guidata Genera script||Sì
|Importazione\esportazione DACPAC||Sì|
|Proprietà degli oggetti||Sì|
|Progettazione tabelle||Sì|

### <a name="query-editor"></a>Editor di query

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Visualizzatore grafico|Sì||
|Esportazione risultati in CSV, JSON, XLSX|Sì||
|IntelliSense|Sì|Sì|
|Frammenti di codice|Sì|Sì|
|Showplan|Anteprima|Sì|
|Statistiche client||Sì|
|Statistiche sulle query dinamiche||Sì|
|Opzioni query||Sì|
|Risultati in un file||Sì|
|Risultati in formato testo||Sì|
|Visualizzatore spaziale||Sì|
|SQLCMD||Sì|
|Debugger Transact-SQL||Sì|

### <a name="operating-system-support"></a>Supporto nei sistemi operativi

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|Sì|Sì|
|macOS|Sì||
|Linux|Sì||

### <a name="data-engineering"></a>Ingegneria dei dati

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Procedura guidata dati esterni|Anteprima||
|Integrazione HDFS|Anteprima||
|Notebooks|Anteprima||

### <a name="database-administration"></a>Amministrazione del database

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Backup/ripristino|Sì|Sì|
|Importazione file flat|Anteprima|Sì|
|SQL Agent|Anteprima|Sì|
|SQL Profiler|Anteprima|Sì|
|Always On||Sì|
|Always Encrypted||Sì|
|Procedura guidata Copia dati||Sì|
|Ottimizzazione guidata dati||Sì|
|Diagrammi di database||Sì|
|Visualizzatore log degli errori||Sì|
|Piani di manutenzione||Sì|
|Query multiserver||Sì|
|Gestione basata su criteri||Sì|
|PolyBase||Sì|
|Archivio query||Sì|
|Server registrati||Sì|
|Replica||Sì|
|Gestione della sicurezza||Sì|
|Broker di servizio||Sì|
|SQL Mail||Sì|
|Esplora modelli||Sì|
|Valutazione della vulnerabilità||Sì|
|Gestione XEvent||Sì|


## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>In Azure Data Studio manca una funzionalità che si trova in SSMS/SSDT. Verrà aggiunta?

Dipende dallo scenario e dalle esigenze del cliente o dell'azienda. Per contribuire alla definizione delle priorità, presentare un suggerimento su [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>Ho compreso che Azure Data Studio e l'estensione mssql per VS Code sono basate su un nuovo servizio strumenti che, dietro le quinte, usa le API SMO. SMO è disponibile in Linux e macOS?

Le API SMO non sono ancora disponibili in Linux o macOS in formato utilizzabile. Un subset delle API SMO necessarie per Azure Data Studio è stato convertito in .NET Core ed è prevista un'espansione nell'ambito della roadmap. Il servizio SQL Tools è su GitHub: [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>È prevista la conversione delle API DACFx e/o di sqlpackage.exe e/o di SSDT per Linux e macOS?

È prevista nella roadmap a lungo termine. Per contribuire alla definizione delle priorità, presentare un suggerimento su [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>I cmdlet SQL PowerShell saranno disponibili in Linux e macOS?

SQL PowerShell è attualmente disponibile in PowerShell Gallery ed è possibile usarlo in Windows per lavorare con SQL Server in esecuzione ovunque, incluso SQL in Linux. L'offerta dei cmdlet SQL PowerShell in Linux e macOS è prevista nella roadmap. Per contribuire alla definizione delle priorità, presentare un suggerimento su [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="who-usually-uses-azure-data-studio"></a>Chi usa in genere Azure Data Studio?

I normali utenti di Azure Data Studio sono sviluppatori e amministratori di database.

## <a name="does-azure-data-studio-integrate-with-azure-sql-data-warehouse"></a>Azure Data Studio si integra con Azure SQL Data Warehouse?

Sì. Attualmente il supporto di Azure Data Studio per Azure SQL Data Warehouse è disponibile in anteprima, insieme a Istanza gestita di database SQL di Azure e ai Big Data di SQL Server 2019.

## <a name="why-is-azure-data-studio-important-for-the-new-version-of-sql-server"></a>Perché Azure Data Studio è importante per la nuova versione di SQL Server?

Man mano che SQL Server estende le proprie funzionalità nello spazio dei Big Data, sono necessari nuovi strumenti per supportare questi casi d'uso. Per questo motivo, Azure Data Studio attualmente fornisce una nuova esperienza di anteprima di supporto per i Big Data di SQL Server, che include la prima esperienza di tipo notebook in assoluto nel set di strumenti SQL Server e una nuova procedura guidata di creazione tabella esterna, che consente di accedere ai dati da istanze remote di Oracle e SQL Server in modo semplice e veloce.
