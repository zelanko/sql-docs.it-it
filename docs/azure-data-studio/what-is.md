---
title: Informazioni su Azure Data Studio
titleSuffix: Azure Data Studio
description: Azure Data Studio è uno strumento gratuito e leggero per la gestione di SQL Server, database SQL di Azure e Azure SQL Data Warehouse, che viene eseguito in Windows, macOS e Linux.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: overview
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.openlocfilehash: 1dd66b432ff489b5576b9ce7f69c1860cb9240d5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958939"
---
# <a name="what-is-azure-data-studio"></a>Che cos'è Azure Data Studio?

Azure Data Studio è uno strumento di database multipiattaforma per professionisti della gestione di dati che usano la famiglia Microsoft di piattaforme dati locali e cloud in Windows, MacOS e Linux.

Precedentemente rilasciato con il nome di anteprima di SQL Operations Studio, Azure Data Studio offre un'esperienza di modifica moderna per la gestione dei dati tra più origini con funzionalità IntelliSense, frammenti di codice, integrazione del controllo del codice sorgente e un terminale integrato. Azure Data Studio è stato progettato in base alle esigenze dell'utente della piattaforma dati, con grafici predefiniti di set di risultati delle query e dashboard personalizzabili.

**[Scaricare e installare [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="sql-code-editor-with-intellisense"></a>Editor di codice SQL con IntelliSense

[!INCLUDE[name-sos](../includes/name-sos-short.md)] offre un'esperienza di codifica SQL moderna e incentrata sulla tastiera che semplifica le attività quotidiane grazie a funzionalità integrate quali finestre a più schede, un editor SQL avanzato, IntelliSense, completamento delle parole chiave, frammenti di codice, esplorazione del codice e integrazione del controllo del codice sorgente (Git). Consente di eseguire query SQL su richiesta e visualizzare e salvare i risultati come testo, JSON o Excel, oltre che modificare i dati, organizzare le connessioni ai database preferiti e sfogliare gli oggetti di database in un'esperienza di esplorazione familiare. Per informazioni su come usare l'editor SQL, vedere [Usare l'editor SQL per creare oggetti di database](tutorial-sql-editor.md).

## <a name="smart-sql-code-snippets"></a>Frammenti di codice SQL intelligenti

I frammenti di codice SQL generano la sintassi SQL appropriata per creare database, tabelle, viste, stored procedure, utenti, accessi, ruoli e così via, nonché aggiornare gli oggetti di database esistenti. Usare i frammenti di codice intelligenti per creare rapidamente copie del database a scopo di sviluppo o test e per generare ed eseguire script di creazione e inserimento.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] fornisce anche funzionalità per la creazione di frammenti di codice SQL personalizzati. Per altre informazioni, vedere [Creare e usare frammenti di codice](code-snippets.md).


## <a name="customizable-server-and-database-dashboards"></a>Dashboard di server e database personalizzabili

È possibile creare dashboard avanzati e personalizzabili per monitorare e risolvere rapidamente i colli di bottiglia delle prestazioni nei database. Per informazioni sui widget di informazioni dettagliate e sui dashboard per database e server, vedere [Gestire server e database con i widget di informazioni dettagliate](insight-widgets.md).

## <a name="connection-management-server-groups"></a>Gestione delle connessioni (gruppi di server)

I gruppi di server consentono di organizzare le informazioni di connessione per i server e i database che si utilizzano. Per informazioni dettagliate, vedere [Gruppi di server](server-groups.md).

## <a name="integrated-terminal"></a>Terminale integrato

Nella finestra del terminale integrato all'interno dell'interfaccia utente di [!INCLUDE[name-sos](../includes/name-sos-short.md)] si possono usare i propri strumenti da riga di comando preferiti, ad esempio Bash, PowerShell, sqlcmd, bcp e ssh. Per informazioni sul terminale integrato, vedere [Terminale integrato](integrated-terminal.md).

## <a name="extensibility-and-extension-authoring"></a>Estendibilità e creazione di estensioni

È possibile migliorare l'esperienza di [!INCLUDE[name-sos](../includes/name-sos-short.md)] estendendo le funzionalità dell'installazione di base. [!INCLUDE[name-sos](../includes/name-sos-short.md)] fornisce punti di estendibilità per le attività di gestione dei dati, oltre al supporto per la creazione di estensioni.

Per informazioni sull'estendibilità in [!INCLUDE[name-sos](../includes/name-sos-short.md)], vedere [Estendibilità](extensibility.md).
Per informazioni sulla creazione di estensioni, vedere [Creazione di estensioni](extension-authoring.md).

## <a name="feature-comparison-with-sql-server-management-studio-ssms"></a>Confronto delle funzionalità con Server Management Studio (SSMS)

**Usare Azure Data Studio se:**
- L'ambiente di esecuzione è macOS o Linux
- Ci si connette a un cluster Big Data di SQL Server 2019
- Si dedica la maggior parte del tempo alla modifica o all'esecuzione di query
- È necessario poter creare rapidamente grafici e visualizzare i set di risultati
- Si può eseguire la maggior parte delle attività amministrative tramite il terminale integrato usando sqlcmd o PowerShell
- Si ha una necessità minima di esperienze di tipo procedura guidata
- Non è necessario eseguire una configurazione amministrativa completa

**Usare SQL Server Management Studio se:**
- Si dedica la maggior parte del tempo ad attività di amministrazione di database
- Si esegue una configurazione amministrativa completa
- Ci si occupa di gestione della sicurezza, incluse gestione degli utenti, valutazione della vulnerabilità e configurazione delle funzionalità di sicurezza
- Si usano i report per SQL Server Query Store
- È necessario usare dashboard e procedure guidate di ottimizzazione delle prestazioni
- Si esegue l'importazione/esportazione di file DACPAC
- È necessario accedere ai server registrati e si vogliono controllare i servizi di SQL Server in Windows

### <a name="shell"></a>Shell

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Accesso ad Azure|Sì|Sì|
|Dashboard|Sì||
|Estensioni|Sì||
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
|Procedura guidata Genera script||Sì|
|Importazione\esportazione DACPAC||Sì|
|Proprietà degli oggetti||Sì|
|Progettazione tabelle||Sì|


### <a name="query-editor"></a>Editor query

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

### <a name="operating-system-support"></a>Supporto nei sistemi operativi

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Linux|Sì||
|macOS|Sì||
|Windows|Sì|Sì|

### <a name="data-engineering"></a>Ingegneria dei dati

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Procedura guidata di creazione tabella esterna|Anteprima||
|Integrazione HDFS|Anteprima||
|Blocchi appunti|Anteprima||

### <a name="database-administration"></a>Amministrazione del database

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Backup/ripristino|Sì|Sì|
|Importazione file flat|Anteprima|Sì|
|SQL Agent|Anteprima|Sì|
|SQL Profiler|Anteprima|Sì|
|Always On||Sì|
|Crittografia sempre attiva||Sì|
|Procedura guidata Copia dati||Sì|
|Ottimizzazione guidata dati||Sì|
|Visualizzatore log degli errori||Sì|
|Piani di manutenzione||Sì|
|Query multiserver||Sì|
|Gestione basata su criteri||Sì|
|PolyBase||Sì|
|Archivio query||Sì|
|Server registrati||Sì|
|Replica||Sì|
|Gestione della sicurezza||Sì|
|Service Broker||Sì|
|SQL Mail||Sì|
|Esplora modelli||Sì|
|Valutazione della vulnerabilità||Sì|
|Gestione XEvent||Sì|

## <a name="next-steps"></a>Passaggi successivi

- [Scaricare e installare [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [Connettersi ed eseguire query in SQL Server](quickstart-sql-server.md)
- [Connettersi ed eseguire query nel database SQL di Azure](quickstart-sql-database.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
