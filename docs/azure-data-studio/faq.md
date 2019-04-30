---
title: DOMANDE FREQUENTI
titleSuffix: Azure Data Studio
description: Domande frequenti (FAQ) su Azure Data Studio.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 129e7de66e896e1f452c5d68fc4891d9cc5eafa3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238292"
---
# <a name="includeazure-data-studioincludesname-sosmd-faq"></a>Domande frequenti su [!INCLUDE[Azure Data Studio](../includes/name-sos.md)]

## <a name="what-is-azure-data-studio"></a>Che cos'è Azure Data Studio?

Azure Data Studio viene aperto un nuovo codice sorgente, l'ambiente desktop multipiattaforma per i professionisti di dati utilizzando la famiglia di dati di Azure in locale e cloud piattaforme di dati in Windows, MacOS e Linux. Rilasciato in precedenza con il nome di anteprima di SQL Operations Studio, un moderno editor esperienza con offerte di Studio di Azure Data fulmine rapide IntelliSense, frammenti di codice, integrazione del controllo codice sorgente e un terminale integrato. È progettato con l'utente di piattaforma di dati presente, con compilato nella creazione di grafici di set di risultati di query e dashboard personalizzabili.

Research ha dimostrato che gli utenti impiegano un ordine di grandezza più tempo a lavorare in modalità di modifica query rispetto a qualsiasi altra attività con SQL Server Management Studio. Per questo motivo, Azure Data Studio è stato progettato per dedicarsi eccessivamente le funzionalità che vengono utilizzati più, con esperienze aggiuntive rese disponibili come estensioni facoltative nel prodotto. In questo modo tutti gli utenti di personalizzare l'ambiente per i flussi di lavoro che usano più spesso.


## <a name="how-much-does-azure-data-studio-cost"></a>Quanto costa Azure dati Studio?

Data Studio di Azure è gratuito per uso commerciale o privato.

## <a name="who-should-use-azure-data-studio"></a>Chi dovrebbe utilizzare Data Studio di Azure

Chiunque può utilizzare Data Studio di Azure. Tuttavia, è progettato per semplificare le attività eseguite per gli sviluppatori di database, gli amministratori di database, gli amministratori di sistema e fornitori di software indipendenti.

## <a name="what-can-i-do-with-azure-data-studio"></a>Che cosa può fare con Azure Data Studio?

Azure Data Studio si basa su Visual Studio Code e offre un leggero, spostarvi lo stato attivo di esperienza di flusso di lavoro di codice moderne, quando si lavora con SQL Server, Database SQL di Azure, Azure SQL Data Warehouse. Azure Data Studio rende le esperienze di core che affidano ogni giorno semplice e pratici con funzionalità incorporate, ad esempio più finestre scheda, un editor SQL avanzato, IntelliSense, completamento delle parole chiave, frammenti di codice e navigazione nel codice e integrazione del controllo codice sorgente (Git e TFS). È possibile eseguire query a richiesta, visualizzare e salvare i risultati come testo, JSON o Excel, modificare i dati, organizzare e gestire le connessioni ai database preferiti e sfogliare oggetti di database tramite una familiare esperienza di esplorazione.

Usare i tuoi strumenti Preferiti della riga di comando (ad esempio, Bash, PowerShell, sqlcmd, bcp, psql SSH) nella finestra del terminale integrato direttamente nell'interfaccia utente di Studio dei dati di Azure. Genera ed esegui script di CREATE e INSERT per gli oggetti di database al fine di creare copie del database di sviluppo o a scopo di test. Migliora la produttività con frammenti di codice intelligenti e con grafiche ricche ed intuitive per creare nuovi oggetti di database (ad esempio tabelle, viste, stored procedure, utenti, account di accesso, ruoli e così via) o per aggiornare gli oggetti di database esistenti. Utilizza le dashboard personalizzabili al fine di monitorare e risolvere rapidamente eventuali colli di bottiglia nei database locali, in Azure o in qualsiasi cloud.

Azure Data Studio offre un'esperienza coerente per il backup e ripristino dei database. Grazie al supporto pianificato per i gruppi di disponibilità di SQL Server Always-on, si possono facilmente configurare, monitorare e risolvere i problemi di gruppi di disponibilità per i database di SQL Server cruciali e rapidamente il failover a un database secondario durante un'emergenza. Azure Data Studio è stato progettato per aumentare la produttività del ciclo di vita DevOps dei database di scelta nei sistemi operativi di propria scelta. Di conseguenza, ha sempre il controllo e si può ridurre i rischi, risolvere i problemi più rapidamente e offrire continuamente valore che supera le aspettative dei clienti.

## <a name="is-azure-data-studio-open-source"></a>È Open Source di Azure Data Studio?

Il codice sorgente per il provider di dati e Data Studio di Azure è disponibile in GitHub. Il codice sorgente per il front-end Data Studio di Azure (che si basa su Visual Studio Code) è disponibile in un contratto di licenza che fornisce diritti per modificare e utilizzare il software, ma non per ridistribuirlo o inserirlo in un servizio cloud di codice sorgente. Il codice sorgente per i provider di dati è disponibile con licenza MIT in [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-we-plan-to-open-source-ssms"></a>Se si prevede di aprire origine SQL Server Management Studio.

No. Tuttavia, la nuova generazione di CLI e di interfacce utente per gli strumenti con supporto multi-OS sono open source. Ad esempio, l'estensione mssql per Visual Studio Code, mssql scripter e msql-CLI sono tutti open source su GitHub. Il codice sorgente per Azure Data Studio è disponibile in GitHub.  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>Ora che è disponibile Azure Data Studio, Microsoft intende deprecare SSMS e SSDT? 

No. Gli investimenti per i principali strumenti Windows (SQL Server Management Studio, SSDT, PowerShell) continueranno insieme alla nuova generazione di strumenti ed interfacce grafiche multi-OS e multi-DB. L'obiettivo è quello di offrire ai clienti la possibilità di scegliere gli strumenti che desiderano utilizzare sulle piattaforme di propria scelta, in base ai relativi scenari. Azure Data Studio più strettamente riguarda l'esperienza utente per la modifica di query e lo sviluppo di dati, quali la ricerca ha dimostrato è la funzionalità maggiormente usata in SQL Server Management Studio da un ordine di grandezza. Sono disponibili come estensioni in Azure Data Studio anche altre funzionalità amministrative ad alto valore, ad esempio backup, ripristino, gestione dei processi dell'agente e server di profilatura. Azure Data Studio è anche multipiattaforma, che consente agli utenti di lavorare nella piattaforma preferita. Tuttavia, ancora SQL Server Management Studio offre la più ampia gamma di funzioni amministrative e rimane lo strumento principale per le attività di gestione della piattaforma. 

## <a name="when-should-i-use-azure-data-studio-vs-sql-server-management-studio"></a>Quando è consigliabile usare Azure Data Studio e SQL Server Management Studio?

*Usare Azure Data Studio se è:*

- Per la maggior parte del tempo di modifica o l'esecuzione di query.
- Necessario saper rapidamente del grafico e visualizzare i set di risultati.
- Può eseguire la maggior parte delle attività amministrative tramite il terminale integrato con sqlcmd o Powershell.
- Sono necessari minimo esperienze di procedura guidata.
- Non è necessario eseguire avanzato amministrativo o configurazione correlati della piattaforma.
- Necessario per l'esecuzione in macOS o Linux.

*Usare SQL Server Management Studio se è:*

- Per la maggior parte del tempo in attività di amministrazione del database.
- Esegue una configurazione complessa amministrativa o dalla piattaforma.
- Esegue Gestione della sicurezza, inclusi gestione degli utenti, la valutazione della vulnerabilità e configurazione delle funzionalità di sicurezza.
- Necessario rendere utilizzare dei consulenti di ottimizzazione delle prestazioni e i dashboard.
- Usare i diagrammi di database e le finestre di progettazione di tabella.
- Sta eseguendo l'importazione/esportazione di dacpac.
- Devono poter accedere a server registrati.
- Assicurarsi di utilizzare la modalità sqlcmd, in tempo reale delle statistiche di query o le statistiche client.

## <a name="feature-comparison"></a>Confronto delle funzionalità

### <a name="shell-features"></a>Funzionalità della shell

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Sign-In Azure|Yes|Yes|
|Dashboard|Yes| |
|Estensioni|Yes| |
|Terminale integrato|Yes||
|Esplora oggetti|Yes|Yes|
|Scripting per gli oggetti|Yes|Yes|
|Sistema di progetto|Yes||
|Selezionare dalla tabella|Yes|Yes|
|Controllo del codice sorgente|Yes||
|Riquadro attività|Yes||
|Utilizzo dei temi|Yes||
|Modalità scura|Yes||
|Esplora risorse di Azure|Anteprima||
|Procedura guidata Genera script||Yes
|Importazione/esportazione con estensione DACPAC||Yes|
|Proprietà degli oggetti||Yes|
|Progettazione tabelle||Yes|

### <a name="query-editor"></a>Editor query

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Visualizzatore grafico|Yes||
|Esportare i risultati in CSV, JSON, con estensione XLSX|Yes||
|IntelliSense|Yes|Yes|
|Frammenti di codice|Yes|Yes|
|Visualizza il piano|Anteprima|Yes|
|Statistiche client||Yes|
|Statistiche sulle Query dinamiche||Yes|
|Opzioni query||Yes|
|Risultati in un file||Yes|
|Risultati in formato testo||Yes|
|Visualizzatore spaziale||Yes|
|SQLCMD||Yes|
|Debugger Transact-SQL||Yes|

### <a name="operating-system-support"></a>Supporto nei sistemi operativi

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|Yes|Yes|
|macOS|Yes||
|Linux|Yes||

### <a name="data-engineering"></a>Il data Engineering

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Procedura guidata di dati esterni|Anteprima||
|Integrazione di HDFS|Anteprima||
|Blocchi appunti|Anteprima||

### <a name="database-administration"></a>Amministrazione del database

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Backup / ripristino|Yes|Yes|
|Importa File flat|Anteprima|Yes|
|SQL Agent|Anteprima|Yes|
|SQL Profiler|Anteprima|Yes|
|Always On||Yes|
|Crittografia sempre attiva||Yes|
|Copia dati guidata||Yes|
|I dati dello strumento ottimizzazione guidata||Yes|
|Diagrammi di database||Yes|
|Visualizzatore Log di errore||Yes|
|Piani di manutenzione||Yes|
|Multi-Server Query||Yes|
|Gestione basata su criteri||Yes|
|PolyBase||Yes|
|Archivio query||Yes|
|Server registrati||Yes|
|Replica||Yes|
|Gestione della sicurezza||Yes|
|Service Broker||Yes|
|SQL Mail||Yes|
|Esplora modelli||Yes|
|Valutazione della vulnerabilità||Yes|
|Gestione di XEvent||Yes|


## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>Azure Data Studio manca una funzionalità che si trova in SSMS o SSDT. Verrà aggiunta?

A seconda dello scenario e delle necessità del cliente/business. Per aiutare a definire la priorità, invia un suggerimento in [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>Sono consapevole di Studio di Azure Data e l'estensione mssql per Visual Studio Code sono basate su un nuovo servizio di strumenti che usa le API SMO dietro le quinte. SMO è disponibile in Linux e macOS?

Le API di SMO non sono ancora utilizzabili in Linux o macOS. Viene trasferita su un sottoinsieme delle API SMO per .NET Core che è necessaria per Azure Data Studio e si prevede di espandere come parte del piano. Il servizio di strumenti di SQL è disponibile su GitHub: [ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>È prevista la conversione di DACFx APIs e/o sqlpackage.exe e/o SSDT per Linux e macOS?

È sulla roadmap a lungo termine. Per aiutare a definire la priorità, invia un suggerimento in [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>I cmdlet di PowerShell per SQL sarà disponibili in Linux e macOS?

PowerShell per SQL è attualmente disponibile nella PowerShell gallery ed è possibile utilizzarlo in Windows con SQL Server in esecuzione in qualsiasi posizione, incluso su Linux. Rendere disponibili le cmdlet PowerShell di SQL su Linux e macOS è nella roadmap. Per aiutare a definire la priorità, invia un suggerimento in [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="who-usually-uses-azure-data-studio"></a>Chi usa in genere Data Studio di Azure?

Gli sviluppatori e amministratori di database sono in genere gli utenti di Azure Data Studio.

## <a name="does-azure-data-studio-integrate-with-azure-sql-data-warehouse"></a>Studio di dati di Azure è integrata con Azure SQL Data Warehouse?

Sì. Supporto di Azure Data Studio per Azure SQL Data Warehouse è attualmente in anteprima, insieme a istanza gestita di Database di Azure SQL e SQL Server 2019 Big Data.

## <a name="why-is-azure-data-studio-important-for-the-new-version-of-sql-server"></a>Perché è importante per la nuova versione di SQL Server Data Studio di Azure?

SQL Server estende le funzionalità nello spazio di Big Data, è necessario nuovi strumenti per supportare i casi d'uso. Per questo motivo, Studio di Azure Data oggi è destinato ad una nuova esperienza di anteprima del supporto per i Big Data di SQL Server, tra cui il primo mai esperienza notebook in una nuova procedura guidata Create External Table che effettua l'accesso ai dati da SQL remoto e il set di strumenti di SQL Server Istanze server e Oracle facile e veloce.
