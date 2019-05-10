---
title: Panoramica
titleSuffix: Azure Data Studio
description: Azure Data Studio è uno strumento gratuito, leggero, che viene eseguito in Windows, macOS e Linux, per la gestione di SQL Server, Database SQL di Azure e Azure SQL Data Warehouse.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: overview
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 1b64b8d23ce58fda704926affdea1103afae0e91
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089496"
---
# <a name="what-is-azure-data-studio"></a>Che cos'è Azure Data Studio?

Azure Data Studio è un multipiattaforma database dello strumento per i professionisti di dati utilizzando la famiglia Microsoft di un'istanza locale e cloud piattaforme di dati in Windows, MacOS e Linux.

Rilasciato in precedenza con il nome di anteprima di SQL Operations Studio, Studio di Azure Data offre un'esperienza moderna editor con Intellisense, frammenti di codice, integrazione del controllo codice sorgente e un terminale integrato. È progettato con l'utente di piattaforma di dati presente, con compilato nella creazione di grafici di set di risultati di query e dashboard personalizzabili.

**[Scaricare e installare [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="sql-code-editor-with-intellisense"></a>Editor di codice SQL grazie a IntelliSense

[!INCLUDE[name-sos](../includes/name-sos-short.md)] offre un linguaggio SQL moderno, incentrato sulla tastiera esperienza che agevola le attività quotidiane con funzionalità incorporate, ad esempio più finestre scheda, un editor SQL avanzato, IntelliSense, completamento delle parole chiave, frammenti di codice, esplorazione del codice e controllo del codice sorgente di codifica integrazione (Git). Eseguire query SQL su richiesta, visualizzare e salvare i risultati di tipo text, JSON o Excel. Modificare i dati, organizzare le connessioni di database Preferiti e sfogliare oggetti di database in un oggetto familiarità esperienza di esplorazione. Per informazioni su come usare l'editor SQL, vedere [usare l'editor SQL per creare oggetti di database](tutorial-sql-editor.md).

## <a name="smart-sql-code-snippets"></a>Frammenti di codice SQL intelligenti

Frammenti di codice SQL generano la sintassi SQL appropriata per creare database, tabelle, viste, stored procedure, gli utenti, account di accesso, ruoli, e così via e per aggiornare gli oggetti di database esistenti. E' possibile utilizzare i frammenti di codice smart per creare rapidamente copie del database in fase di sviluppo o test, e per generare ed eseguire script di CREATE e INSERT.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] fornisce anche funzionalità per creare frammenti di codice SQL personalizzati. Per altre informazioni, vedere [creazione e uso di frammenti di codice](code-snippets.md).


## <a name="customizable-server-and-database-dashboards"></a>Dashboard di server e database personalizzabili

È possibile creare dashboard avanzati e personalizzabili per monitorare e risolvere rapidamente i colli di bottiglia delle prestazioni del database. Per informazioni sui widget insight e sui dashboard di database (e server) vedere [Gestire server e i database con i widget insight](insight-widgets.md).

## <a name="connection-management-server-groups"></a>Gestione delle connessioni (gruppi di server)

I gruppi di server consentono di organizzare le informazioni di connessione per i server e i database su cui si lavora. Per informazioni dettagliate, vedere [Gruppi di server](server-groups.md).

## <a name="integrated-terminal"></a>Terminale integrato

È possibile utilizzare gli strumenti da riga di comando (ad esempio, Bash, PowerShell, sqlcmd, bcp e ssh) nella finestra del terminale integrata direttamente nell'interfaccia utente di [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Per scoprire il terminale integrato, vedere [terminale integrato](integrated-terminal.md).

## <a name="extensibility-and-extension-authoring"></a>Estendibilità e la creazione di estensione

Migliorare il [!INCLUDE[name-sos](../includes/name-sos-short.md)] esperienza estendendo le funzionalità dell'installazione di base. [!INCLUDE[name-sos](../includes/name-sos-short.md)] fornisce punti di estendibilità per le attività di gestione, nonché il supporto per la creazione di estensione.

Per informazioni sulle estendibilità [!INCLUDE[name-sos](../includes/name-sos-short.md)], vedere [estendibilità](extensibility.md).
Per altre informazioni sulla creazione di estensioni, vedere [Extension authoring](extension-authoring.md).

## <a name="feature-comparison-with-sql-server-management-studio-ssms"></a>Confronto delle funzionalità con SQL Server Management Studio (SSMS)

**Usare Azure Data Studio se è:**
- Dovranno essere eseguiti in macOS o Linux
- Si connette a un cluster di big data di SQL Server 2019
- Per la maggior parte del tempo di modifica o l'esecuzione di query
- Devono poter rapidamente del grafico e visualizzare i set di risultati
- Possono eseguire la maggior parte delle attività amministrative tramite il terminale integrato con sqlcmd o Powershell
- Sono necessari minimo esperienze di procedura guidata
- Non è necessario apportare modifiche alla configurazione profonde amministrativi

**Usare SQL Server Management Studio se è:**
- Per la maggior parte del tempo in attività di amministrazione del database
- Esegue configurazione profonde amministrativo
- Esegue Gestione della sicurezza, inclusi gestione degli utenti, la valutazione della vulnerabilità e configurazione delle funzionalità di sicurezza
- Usare i report per SQL Server Query Store
- Necessario rendere utilizzare dei consulenti di ottimizzazione delle prestazioni e i dashboard
- Esegue importazione/esportazione di dacpac
- Accedere a server registrati e per SQL Server di controllo servizi su Windows

### <a name="shell"></a>Shell

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Sign-In Azure|Yes|Yes|
|Dashboard|Yes||
|Estensioni|Yes||
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
|Procedura guidata Genera script||Yes|
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

### <a name="operating-system-support"></a>Supporto nei sistemi operativi

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Linux|Yes||
|macOS|Yes||
|Windows|Yes|Yes|

### <a name="data-engineering"></a>Il data Engineering

|Funzionalità|Azure Data Studio|SSMS|
|:---|:---|:---|
|Creazione guidata tabella esterna|Anteprima||
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



## <a name="next-steps"></a>Passaggi successivi
- [Scaricare e installare [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [Connettersi ed eseguire query di SQL Server](quickstart-sql-server.md)
- [Connettersi ed eseguire query su Database SQL di Azure](quickstart-sql-database.md)
