---
title: Log operazioni in Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: aa1db060-95dc-4198-8aeb-cffdda44b140
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58169ffcc696c87addee0417700ba131a71e12f0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62703308"
---
# <a name="log-operations-in-analysis-services"></a>Registrare le operazioni in Analysis Services
  Un'istanza di Analysis Services registrerà le notifiche di server, errori e avvisi per il file msmdsrv log: uno per ogni istanza installata. Gli amministratori fanno riferimento a questo log per informazioni sulla routine nonché per eventi straordinari. Nelle versioni recenti la registrazione è stata migliorata per includere altre informazioni. I record di log includono ora informazioni sull'edizione e la versione del prodotto, nonché eventi del processore, della memoria, della connettività e di blocco. È possibile consultare l'elenco completo delle modifiche in [Miglioramenti della registrazione](https://support.microsoft.com/kb/2965035).  
  
 Oltre alla funzionalità di registrazione predefinita, molti amministratori e sviluppatori usano anche gli strumenti forniti dalla community di Analysis Services, ad esempio **ASTrace**, per raccogliere i dati relativi alle operazioni del server. Vedere [esempi della Community di Microsoft SQL Server: Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/) collegamenti per il download.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
-   [Posizione e tipi di log](#bkmk_location)  
  
-   [Informazioni generali sulle impostazioni di configurazione dei file di log](#bkmk_general)  
  
-   [File di log del servizio MSMDSRV](#bkmk_msmdsrv)  
  
-   [Log di query](#bkmk_querylog)  
  
-   [File di minidump (con estensione mdmp)](#bkmk_mdmp)  
  
-   [Suggerimenti e procedure consigliate](#bkmk_tips)  
  
> [!NOTE]  
>  Per informazioni sulla registrazione, potrebbe essere utile interessarsi alle operazioni di traccia che mostrano i percorsi di elaborazione e di esecuzione delle query. Oggetti di traccia per analisi ad hoc e prolungate (come il controllo dell'accesso ai cubi) ai, nonché indicazioni su come utilizzare al meglio registratore di volo e SQL Server Profiler XEvent sono disponibili ai tramite i collegamenti in questa pagina: [Monitorare un'istanza di Analysis Services](monitor-an-analysis-services-instance.md).  
  
##  <a name="bkmk_location"></a> Posizione e tipi di log  
 Analysis Services fornisce i log descritti di seguito.  
  
|Posizione o nome del file|Tipo|Utilizzo|Attivato per impostazione predefinita|  
|---------------------------|----------|--------------|-------------------|  
|Msmdsrv.log|Log degli errori|Monitoraggio della routine e risoluzione dei problemi di base|Yes|  
|Tabella OlapQueryLog in un database relazionale|Log di query|Raccolta di input per l'Ottimizzazione guidata basata sulle statistiche di utilizzo|No|  
|File SQLDmp\<guid > i file con estensione mdmp|Arresti anomali ed eccezioni|Risoluzione dei problemi completa|No|  
  
 È consigliabile il collegamento seguente per le risorse di informazioni aggiuntive non trattate in questo argomento: [Suggerimenti di raccolta dati dal supporto Microsoft iniziale](https://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx).  
  
##  <a name="bkmk_general"></a> Informazioni generali sulle impostazioni di configurazione dei file di log  
 È possibile trovare le sezioni per ogni log nel file di configurazione del server msmdsrv.ini, che si trova nella cartella \Programmi\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP\Config. Visualizzare [Configure Server Properties in Analysis Services](../server-properties/server-properties-in-analysis-services.md) per istruzioni sulla modifica del file.  
  
 Dove possibile, è consigliabile impostare le proprietà di registrazione nella pagina delle proprietà del server di Management Studio. Anche se in alcuni casi sarà necessario modificare il file msmdsrv.ini direttamente per configurare le impostazioni che non sono visibili negli strumenti di amministrazione.  
  
 ![Sezione del file di configurazione con le impostazioni del registro](../media/ssas-logfilesettings.png "sezione del file di configurazione con le impostazioni del log")  
  
##  <a name="bkmk_msmdsrv"></a> File di log del servizio MSMDSRV  
 Analysis Services registra le operazioni del server nel file msmdsrv.log, uno per ogni istanza, che si trova in \Programmi\Microsoft SQL Server\\<istanza\>\Olap\Log.  
  
 Questo file di log viene svuotato a ogni riavvio del servizio. Nelle versioni precedenti, gli amministratori a volte riavviavano il servizio al solo scopo di svuotare il file di log prima che diventasse talmente grande da non poter essere usato. Ciò non è più necessario. Le impostazioni di configurazione introdotte in SQL Server 2012 SP2 e versioni successive consentono di controllare le dimensioni del file di log e la relativa cronologia:  
  
-   `MaxFileSizeMB` Specifica una dimensione massima in megabyte. L'impostazione predefinita è 256. Un valore di sostituzione valido deve essere un numero intero positivo. Quando viene raggiunto il valore `MaxFileSizeMB`, Analysis Services rinomina il file corrente come file msmdsrv{timestamp corrente}.log e inizia un nuovo file msmdsrv.log.  
  
-   `MaxNumberFiles` Specifica la memorizzazione dei file di log meno recenti. Il valore predefinito è 0 (disabilitata). È possibile modificare tale valore con un numero intero positivo per mantenere le versioni del file di log. Quando viene raggiunto il valore `MaxNumberFiles`, Analysis Services elimina il file che contiene nel nome il timestamp meno recente.  
  
 Per usare queste impostazioni, eseguire le operazioni seguenti:  
  
1.  Aprire msmdsrv.ini nel Blocco note.  
  
2.  Copiare le due righe seguenti:  
  
    ```  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    ```  
  
3.  Incollare le due righe nella sezione Log di msmdsrv.ini, sotto il nome del file msmdsrv.log. Entrambe le impostazioni devono essere aggiunte manualmente. Non ci sono segnaposti nel file msmdsrv.ini.  
  
     Il file di configurazione modificato sarà simile al seguente:  
  
    ```  
    <Log>  
    <File>msmdsrv.log</File>  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    <FileBufferSize>0</FileBufferSize>  
  
    ```  
  
4.  Modificare i valori se quelli forniti sono diversi da quelli desiderati.  
  
5.  Salvare il file.  
  
6.  Riavviare il servizio.  
  
##  <a name="bkmk_querylog"></a> Log di query  
 Log di query è in realtà un nome improprio, perché l'attività di query MDX o DAX degli utenti non viene registrata. Raccoglie invece i dati sulle query generate da Analysis Services, che verranno usati successivamente come input di dati nell'Ottimizzazione guidata basata sulle statistiche di utilizzo. I dati raccolti nel log di query non vengono usati per l'analisi diretta. In particolare, i set di dati vengono descritti in matrici di bit, con uno zero o un uno che indica le parti del set di dati incluso nella query. Questi dati saranno usati per la procedura guidata.  
  
 Per il monitoraggio delle query e la risoluzione dei problemi, molti sviluppatori e amministratori usano uno strumento della community, **ASTrace**, per monitorare le query. È anche possibile usare SQL Server Profiler, XEvent o una traccia di Analysis Services. Per i collegamenti correlati alle tracce, vedere [Monitorare un'istanza di Analysis Services](monitor-an-analysis-services-instance.md) .  
  
 Quando è necessario usare il log di query? È consigliabile abilitare il log di query come parte del processo di ottimizzazione delle prestazioni di esecuzione delle query che include l'Ottimizzazione guidata basata sulle statistiche di utilizzo. Il log di query non esiste fino a quando non viene abilitata la funzionalità, non vengono create le strutture di dati per supportarla e non vengono impostate le proprietà usate da Analysis Services per individuare e popolare il log.  
  
 Per abilitare il file di log, attenersi alla procedura seguente:  
  
1.  Creare un database relazionale di SQL Server per archiviare il log di query.  
  
2.  Concedere all'account del servizio di Analysis Services le autorizzazioni sufficienti per il database. L'account richiede le autorizzazioni per creare una tabella, scrivere nella tabella e leggere dalla tabella.  
  
3.  In SQL Server Management Studio fare clic con il pulsante destro del mouse su **Analysis Services** | **Proprietà** | **Generale**e impostare **CreateQueryLogTable** su true.  
  
4.  Facoltativamente, modificare **QueryLogSampling** o **QueryLogTableName** se si vuole eseguire il campionamento delle query con una frequenza diversa o usare un nome diverso per la tabella.  
  
 La tabella del log di query non verrà creata finché non viene eseguito un numero di query MDX sufficiente per soddisfare i requisiti di campionamento. Se ad esempio si mantiene il valore predefinito di 10, è necessario eseguire almeno 10 query prima della creazione della tabella.  
  
 Le impostazioni del log di query sono a livello di server. Le impostazioni specificate verranno usate da tutti i database in esecuzione in questo server.  
  
 ![Query sulle impostazioni del registro in Management Studio](../media/ssas-querylogsettings.png "impostazioni di log di Query in Management Studio")  
  
 Dopo aver specificato le impostazioni di configurazione, eseguire una query MDX più volte. Se il campionamento è impostato su 10, eseguire la query 11 volte. Verificare che la tabella sia stata creata. In Management Studio connettersi al motore di database relazionale, aprire la cartella del database, aprire la cartella **Tabelle** e verificare che **OlapQueryLog** sia presente. Se la tabella non viene visualizzata immediatamente, aggiornare la cartella per visualizzare le eventuali modifiche al contenuto.  
  
 Consentire al log di query di raccogliere dati sufficienti per eseguire l'Ottimizzazione guidata basata sulle statistiche di utilizzo. Se i volumi di query sono ciclici, acquisire un volume di traffico sufficiente da avere un set di dati rappresentativo. Per istruzioni su come eseguire la procedura guidata, vedere [Ottimizzazione guidata basata sulle statistiche di utilizzo](https://msdn.microsoft.com/library/ms189706.aspx) .  
  
 Per altre informazioni sulla configurazione del log di query, vedere [Configuring the Analysis Services Query Log](https://technet.microsoft.com/library/Cc917676) (Configurazione del log di query di Analysis Services). Anche se il documento non è recente, la configurazione del log di query non è stata modificata nelle versioni recenti e le informazioni in esso contenute sono ancora valide.  
  
##  <a name="bkmk_mdmp"></a> File di minidump (con estensione mdmp)  
 I file di dump acquisiscono i dati usati per l'analisi di eventi straordinari. Analysis Services genera automaticamente dei minidump (con estensione mdmp) in risposta a un arresto anomalo del server, a un'eccezione e ad alcuni errori di configurazione. La funzionalità è abilitata ma non invia automaticamente le segnalazioni di arresti anomali.  
  
 Le segnalazioni di arresti anomali vengono configurate tramite la sezione Eccezioni nel file msmdsrv.ini. Queste impostazioni controllano la generazione dei file di dump di memoria. Il frammento di codice seguente mostra i valori predefiniti:  
  
```  
<Exception>  
<CreateAndSendCrashReports>1</CreateAndSendCrashReports>  
<CrashReportsFolder/>  
<SQLDumperFlagsOn>0x0</SQLDumperFlagsOn>  
<SQLDumperFlagsOff>0x0</SQLDumperFlagsOff>  
<MiniDumpFlagsOn>0x0</MiniDumpFlagsOn>  
<MiniDumpFlagsOff>0x0</MiniDumpFlagsOff>  
<MinidumpErrorList>0xC1000000, 0xC1000001, 0xC102003F, 0xC1360054, 0xC1360055</MinidumpErrorList>  
<ExceptionHandlingMode>0</ExceptionHandlingMode>  
<CriticalErrorHandling>1</CriticalErrorHandling>  
<MaxExceptions>500</MaxExceptions>  
<MaxDuplicateDumps>1</MaxDuplicateDumps>  
</Exception>  
```  
  
 **Configurare le segnalazioni di arresti anomali**  
  
 Se non diversamente indicato dal supporto tecnico Microsoft, la maggior parte degli amministratori usa le impostazioni predefinite. Questo articolo non recente della Knowledge base viene ancora usato per fornire istruzioni su come configurare i file di dump: [Come configurare Analysis Services per generare file di dump di memoria](https://support.microsoft.com/kb/919711).  
  
 L'impostazione di configurazione che verrà modificata con maggiore probabilità è `CreateAndSendCrashReports`, usata per determinare se verrà generato o meno un file di dump di memoria.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0|Disattiva il file di dump di memoria. Tutte le altre impostazioni nella sezione Eccezioni vengono ignorate.|  
|1|(Impostazione predefinita) Abilita ma non invia il file di dump di memoria.|  
|2|Abilita e invia automaticamente una segnalazione di errore a Microsoft.|  
  
 `CrashReportsFolder` è il percorso dei file di dump. Per impostazione predefinita, il file con estensione mdmp e i record di log associati vengono archiviati nella cartella \Olap\Log.  
  
 `SQLDumperFlagsOn` viene usata per generare un dump completo. Per impostazione predefinita, i dump completi non sono abilitati. È possibile impostare questa proprietà su `0x34`.  
  
 Per altre informazioni generiche, vedere i collegamenti seguenti:  
  
-   [Analisi dei minidump di SQL Server](https://blogs.msdn.com/b/sqlcat/archive/2009/09/11/looking-deeper-into-sql-server-using-minidumps.aspx)  
  
-   [Come creare un file di dump in modalità utente](https://support.microsoft.com/kb/931673)  
  
-   [Come usare l'utilità Sqldumper.exe per generare un file di dump in SQL Server](https://support.microsoft.com/kb/917825)  
  
##  <a name="bkmk_tips"></a> Suggerimenti e procedure consigliate  
 Questa sezione è un riepilogo dei suggerimenti indicati in questo articolo.  
  
-   Configurare il file msmdsrv.log per controllare le dimensioni e il numero di file di log msmdsrv. Le impostazioni non vengono abilitate per impostazione predefinita, pertanto assicurarsi di aggiungerle come passaggio di post-installazione. Vedere [File di log del servizio MSMDSRV](#bkmk_msmdsrv) in questo argomento.  
  
-   Leggere questo post di blog del supporto tecnico Microsoft per informazioni sulle risorse da usare per ottenere informazioni sulle operazioni del server: [Raccolta dati iniziale](https://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)  
  
-   Usare ASTrace2012, anziché un log di query, per identificare gli utenti che eseguono query sui cubi. Il log di query viene usato generalmente per fornire un input all'Ottimizzazione guidata basata sulle statistiche di utilizzo e i dati acquisiti non sono facili da leggere o interpretare. ASTrace2012 è uno strumento della community, ampiamente usato, che acquisisce le operazioni di query. Vedere [esempi della Community di Microsoft SQL Server: Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di un'istanza di Analysis Services](analysis-services-instance-management.md)   
 [Introduzione al monitoraggio di Analysis Services tramite SQL Server Profiler](introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)   
 [Configurare le proprietà del Server in Analysis Services](../server-properties/server-properties-in-analysis-services.md)  
  
  
