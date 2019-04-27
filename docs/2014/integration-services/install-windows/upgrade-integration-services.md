---
title: Aggiornare Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, upgrading
- SSIS, upgrading
- SQL Server Integration Services, upgrading
- upgrading Integration Services
ms.assetid: 04f9863c-ba0b-47c5-af91-f2d41b078a23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d1e40954a5a5eb7a69ba4f70b798356f38175fed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768085"
---
# <a name="upgrade-integration-services"></a>Aggiornare Integration Services
  Se nel computer è installato [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)], è possibile eseguire l'aggiornamento a [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
 Se si esegue l'aggiornamento a [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] in un computer con una di queste versioni precedenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] verrà installato side-by-side con la versione precedente.  
  
 Con l'installazione side-by-side, vengono installate più versioni dell'utilità dtexec. Per assicurarsi di eseguire la versione corretta dell'utilità, al prompt dei comandi eseguirla immettendo il percorso completo (\<unità>:\Programmi\Microsoft SQL Server\\<versione\>\DTS\Binn). Per ulteriori informazioni su dtexec, vedere [dtexec Utility](../packages/dtexec-utility.md).  
  
> [!NOTE]  
>  Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per impostazione predefinita quando si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tutti gli utenti nel gruppo Utenti dispongono di accesso al servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Quando si installa [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], gli utenti non dispongono di accesso al servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Il servizio è protetto per impostazione predefinita. Dopo l'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , l'amministratore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve eseguire lo strumento Configurazione DCOM (Dcomcnfg.exe) per concedere a utenti specifici l'accesso al servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per altre informazioni, vedere [Grant Permissions to Integration Services Service](../grant-permissions-to-integration-services-service.md).  
  
## <a name="before-upgrading-integration-services"></a>Operazioni preliminari per l'aggiornamento di Integration Services  
 Prima di procedere all'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è consigliabile eseguire Preparazione aggiornamento. Preparazione aggiornamento segnala i problemi che potrebbero verificarsi se si esegue la migrazione dei pacchetti esistenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al nuovo formato dei pacchetti utilizzato da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Per altre informazioni, vedere [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
> [!NOTE]
>  Supporto per la migrazione o l'esecuzione di pacchetti Data Transformation Services (DTS) è stato interrotto nella versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Le seguenti funzionalità DTS non sono più utilizzate.  
> 
>  -   DTS Runtime  
> -   API DTS  
> -   Migrazione guidata pacchetti per la migrazione dei pacchetti DTS alla versione successiva di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
> -   Supporto per la gestione di pacchetti DTS in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
> -   Attività Esegui pacchetto DTS 2000  
> -   Analisi di pacchetti DTS in Preparazione aggiornamento.  
> 
>  Per informazioni sulle altre funzionalità non più supportate, vedere [funzionalità di servizi di integrazione non più usate in SQL Server 2014](../discontinued-integration-services-functionality-in-sql-server-2014.md).  
  
## <a name="upgrading-integration-services"></a>aggiornamento di Integration Services  
 È possibile eseguire l'aggiornamento utilizzando uno dei metodi seguenti:  
  
-   Eseguire [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] programma di installazione e selezionare l'opzione **Aggiorna da SQL Server 2005, SQL Server 2008 o SQL Server 2008 R2**, o **[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]**.  
  
-   Eseguire **setup.exe** al prompt dei comandi e specificare il `/ACTION=upgrade` opzione. Per altre informazioni, vedere la sezione "script di installazione per [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]," nella [installare SQL Server 2014 dal Prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
 Non è possibile utilizzare l'aggiornamento per effettuare le azioni seguenti:  
  
-   Riconfigurare un'installazione esistente di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   Passare da una versione a 32 bit a una versione a 64 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o da una versione a 64 bit a una versione a 32 bit.  
  
-   Passare da una versione localizzata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un'altra versione localizzata.  
  
 È possibile scegliere di eseguire l'aggiornamento sia di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che del [!INCLUDE[ssDE](../../includes/ssde-md.md)], solo del [!INCLUDE[ssDE](../../includes/ssde-md.md)]o solo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se si esegue l'aggiornamento solo del [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] continuerà a essere funzionante ma la funzionalità di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] non sarà disponibile. Se si esegue l'aggiornamento solo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] sarà completamente funzionante ma sarà possibile solo archiviare i pacchetti nel file system, a meno che in un altro computer non sia disponibile un'istanza del [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)] .  
  
## <a name="upgrading-both-integration-services-and-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>Aggiornamento di Integration Services e del Motore di database a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 In questa sezione vengono descritti gli effetti di un aggiornamento che utilizza i criteri seguenti:  
  
-   Si aggiornano a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sia [!INCLUDE[ssDE](../../includes/ssde-md.md)] sia un'istanza del [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e l'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] risiedono nello stesso computer.  
  
### <a name="what-the-upgrade-process-does"></a>Operazioni eseguite durante l'aggiornamento  
 Durante il processo di aggiornamento vengono eseguite le attività seguenti:  
  
-   Installazione dei file, del servizio e degli strumenti di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] ([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]). Se sono presenti più istanze di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] nello stesso computer, al primo aggiornamento delle istanze a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verranno installati i file, il servizio e gli strumenti di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
-   Aggiornamento dell'istanza del [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o il [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] per il [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versione.  
  
-   Sposta i dati verso il [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] oppure [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] alle tabelle di sistema il [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] tabelle di sistema, come indicato di seguito:  
  
    -   Spostamento dei pacchetti senza modifiche dalla tabella di sistema msdb.dbo.sysdtspackages90 alla tabella di sistema msdb.dbo.sysssispackages.  
  
        > [!NOTE]  
        >  Benché i dati vengano spostati in una tabella di sistema diversa, il processo di aggiornamento non esegue la migrazione dei pacchetti al nuovo formato.  
  
    -   Spostamento dei metadati delle cartelle dalla tabella di sistema msdb.sysdtsfolders90 alla tabella di sistema msdb.sysssisfolders.  
  
    -   Spostamento dei dati del log dalla tabella di sistema msdb.sysdtslog90 alla tabella di sistema msdb.sysssislog.  
  
-   Rimozione delle tabelle di sistema msdb.sysdts\*90 e delle stored procedure usate per accedervi in seguito allo spostamento dei dati nelle nuove tabelle msdb.sysssis\* . Tuttavia, durante l'aggiornamento la tabella sysdtslog90 viene sostituita con una vista denominata anche sysdtslog90. Questa nuova vista sysdtslog90 espone la nuova tabella di sistema msdb.sysssislog. In questo modo, l'esecuzione dei report basati sulla tabella di log continuerà senza interruzione.  
  
-   Creazione di tre nuovi ruoli predefiniti a livello di database, db_ssisadmin, db_ssisltduser e db_ssisoperator, per il controllo dell'accesso ai pacchetti. I ruoli db_dtsadmin, db_dtsltduser e db_dtsoperator di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non vengono rimossi ma vengono inseriti come membri dei nuovi ruoli corrispondenti.  
  
-   Se il [!INCLUDE[ssIS](../../includes/ssis-md.md)] archivio pacchetti (vale a dire, il percorso del file system gestito dal [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] service) corrisponde al percorso predefinito **server\90**, **\SQL Server\100**, o **\SQL Server\110** spostamento di tali pacchetti nel nuovo percorso predefinito **server\120**.  
  
-   Aggiornamento del file di configurazione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in modo da puntare all'istanza aggiornata del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
### <a name="what-the-upgrade-process-does-not-do"></a>Operazioni non eseguite durante l'aggiornamento  
 Durante il processo di aggiornamento non vengono eseguite le attività seguenti:  
  
-   **Non esiste** rimuovere il [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] servizio.  
  
-   Migrazione dei pacchetti esistenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al nuovo formato dei pacchetti utilizzato da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Per informazioni su come eseguire la migrazione dei pacchetti, vedere [Aggiornare pacchetti di Integration Services](upgrade-integration-services-packages.md).  
  
-   Spostamento dei pacchetti da percorsi del file system diversi dal percorso predefinito aggiunti al file di configurazione del servizio. Se in precedenza il file di configurazione del servizio è stato modificato per aggiungervi altre cartelle del file system, i pacchetti archiviati in tali cartelle non verranno spostati nel nuovo percorso.  
  
-   Aggiornamento del percorso del file system per l'utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dtexec **(dtexec.exe) nei passaggi del processo di** che chiamano direttamente l'utilità **dtexec** . È necessario modificare manualmente questi passaggi del processo per aggiornare il percorso del file system specificando il percorso di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per l'utilità **dtexec** .  
  
### <a name="what-you-can-do-after-upgrading"></a>Operazioni possibili in seguito all'aggiornamento  
 Al termine del processo di aggiornamento, è possibile effettuare le attività seguenti:  
  
-   Eseguire processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per l'esecuzione di pacchetti.  
  
-   Uso [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per gestire [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacchetti archiviati in un'istanza di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. È necessario modificare il file di configurazione del servizio per aggiungere l'istanza di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] all'elenco dei percorsi gestiti dal servizio.  
  
    > [!NOTE]  
    >  Nelle versioni precedenti di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] non è possibile eseguire la connessione al servizio [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] .  
  
-   Identificare la versione dei pacchetti nella tabella di sistema msdb.dbo.sysssispackages controllando il valore nella colonna packageformat. La colonna packageformat della tabella identifica la versione di ogni pacchetto. Il valore 2 nella colonna packageformat indica un pacchetto di [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)], il valore 3 indica un pacchetto di [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]. Fino a quando non si esegue la migrazione dei pacchetti al nuovo formato, il valore nella colonna packageformat non cambia.  
  
-   Non è possibile usare la [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oppure [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] gli strumenti per progettare, eseguire o gestire [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacchetti. Gli strumenti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] includono le rispettive versioni di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'utilità di esecuzione pacchetti (dtexecui.exe). Il processo di aggiornamento non comporta la rimozione di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]strumenti. Non sarà tuttavia possibile utilizzare questi strumenti per continuare a lavorare con i pacchetti di [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] in un server aggiornato.  
  
-   Per impostazione predefinita, in un'installazione dell'aggiornamento, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene configurato in modo da registrare gli eventi correlati all'esecuzione dei pacchetti nel registro eventi delle applicazioni. Questa impostazione potrebbe generare un numero eccesivo di voci nel registro eventi quando si utilizza la funzionalità di raccolta dati di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Gli eventi registrati includono EventID 12288, che indica che il pacchetto è stato avviato ed EventID 12289 che indica che il pacchetto è stato completato. Per arrestare la registrazione di questi due eventi nel registro eventi dell'applicazione, aprire il Registro di sistema per la modifica. Nel Registro di sistema individuare il nodo HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS e modificare il valore di DWORD dell'impostazione LogPackageExecutionToEventLog da 1 a 0.  
  
## <a name="upgrading-only-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>Aggiornamento solo del Motore di database a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 In questa sezione vengono descritti gli effetti di un aggiornamento che utilizza i criteri seguenti:  
  
-   Si aggiorna solo un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Di conseguenza, l'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] è ora un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], mentre l'istanza di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e gli strumenti client sono di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
-   L'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] risiede in un computer, mentre [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e gli strumenti client risiedono in un altro computer.  
  
### <a name="what-you-can-do-after-upgrading"></a>Operazioni possibili in seguito all'aggiornamento  
 Le tabelle di sistema in cui sono archiviati i pacchetti nell'istanza aggiornata del [!INCLUDE[ssDE](../../includes/ssde-md.md)] non corrispondono a quelle utilizzate in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Pertanto, il [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] le versioni di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] non è possibile individuare i pacchetti nelle tabelle di sistema nell'istanza aggiornata del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Poiché tali pacchetti non possono essere individuati, vi sono alcune limitazioni relative alle operazioni che è possibile eseguire:  
  
-   Non è possibile utilizzare gli strumenti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] in altri computer per caricare o gestire i pacchetti dall'istanza aggiornata del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
    > [!NOTE]  
    >  Anche se non è stata ancora eseguita la migrazione al nuovo formato dei pacchetti nell'istanza aggiornata del [!INCLUDE[ssDE](../../includes/ssde-md.md)], tali pacchetti non possono essere individuati dagli strumenti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. I pacchetti, pertanto, non possono essere utilizzati dagli strumenti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
-   Non è possibile usare [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] oppure [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] in altri computer per eseguire i pacchetti archiviati nel database msdb nell'istanza aggiornata del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Non è possibile utilizzare processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in computer con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] per eseguire pacchetti di [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] archiviati nell'istanza aggiornata del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="external-resources"></a>Risorse esterne  
 Intervento nel blog relativo all' [utilizzo delle applicazioni e delle estensioni SSIS personalizzate esistenti in Denali](https://go.microsoft.com/fwlink/?LinkId=238157)sul sito blogs.msdn.com.  
  
  
