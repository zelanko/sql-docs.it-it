---
title: Opzioni di avvio del servizio del motore di database | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- single-user mode [SQL Server], startup option
- overriding default startup options
- minimal configuration mode [SQL Server], startup option
- default startup options
- temporarily override default startup options [SQL Server]
- startup options [SQL Server]
- starting SQL Server, options
ms.assetid: d373298b-f6cf-458a-849d-7083ecb54ef5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 29984a52d711ef02c3c3b640ef8d59323806c2bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62812283"
---
# <a name="database-engine-service-startup-options"></a>Opzioni di avvio del servizio del motore di database
  Le opzioni di avvio consentono di designare determinati percorsi di file necessari in fase di avvio e di specificare alcune condizioni a livello di server. Per la maggior parte degli utenti non è necessario specificare opzioni di avvio a meno che non si debbano risolvere problemi del [!INCLUDE[ssDE](../../includes/ssde-md.md)] o si verifichi un problema insolito e si ricevano istruzioni dal servizio di supporto tecnico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di utilizzare l'opzione di avvio.  
  
> [!WARNING]  
>  L'utilizzo improprio di opzioni di avvio può influire sulle prestazioni del server e impedire l'esecuzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="about-startup-options"></a>Informazioni sulle opzioni di avvio  
 Quando si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il programma di installazione scrive un set di opzioni di avvio predefinite nel Registro di sistema di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Tali opzioni consentono di specificare un file del database master, un file di log del database master o un file di log degli errori alternativo. Se [!INCLUDE[ssDE](../../includes/ssde-md.md)] non è in grado di individuare i file necessario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene avviato.  
  
 Le opzioni di avvio possono essere impostate utilizzando Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Configurazione delle opzioni di avvio del server &#40;Gestione di configurazione SQL Server&#41;](scm-services-configure-server-startup-options.md).  
  
## <a name="list-of-startup-options"></a>Elenco delle opzioni di avvio  
  
|Opzioni di avvio predefinite|Descrizione|  
|-----------------------------|-----------------|  
|**-d**  *master_file_path*|Percorso completo del file del database master (in genere, C:\Programmi\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\master.mdf). Se non si imposta questa opzione, vengono utilizzati i parametri esistenti nel Registro di sistema.|  
|**-e**  *error_log_path*|Percorso completo del file di log degli errori, in genere C:\Programmi\Microsoft SQL Server\MSSQL.*n*\MSSQL\LOG\ERRORLOG). Se non si imposta questa opzione, vengono utilizzati i parametri esistenti nel Registro di sistema.|  
|**-l**  *master_log_path*|Percorso completo del file di log del database master (in genere C:\Programmi\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\mastlog.ldf). Se non si specifica questa opzione, vengono utilizzati i parametri esistenti nel Registro di sistema.|  
  
|Altre opzioni di avvio|Descrizione|  
|---------------------------|-----------------|  
|**-c**|Riduce i tempi necessari per l'avvio quando si avvia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal prompt dei comandi. Il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] viene in genere avviato come servizio chiamando Gestione controllo servizi. Considerato che [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] non viene avviato come servizio quando viene eseguito l'avvio dal prompt dei comandi, usare **-c** per ignorare questo passaggio.|  
|**-f**|Avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la configurazione minima. È utile nel caso in cui l'impostazione di un valore di configurazione, ad esempio un'allocazione eccessiva di memoria, abbia impedito l'avvio del server. L'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la configurazione minima comporta l'attivazione della modalità utente singolo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere la descrizione di **-m** di seguito.|  
|**-g**  *memory_to_reserve*|Specifica un numero intero di megabyte di memoria che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manterrà disponibili per le allocazioni di memoria internamente al processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma esternamente al pool di memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La memoria esterna al pool di memoria è l'area utilizzata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il caricamento di elementi, ad esempio i file con estensione dll delle procedure estese, i provider OLE DB cui fanno riferimento le query distribuite e gli oggetti di automazione cui viene fatto riferimento nelle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] . Il valore predefinito è 256 MB.<br /><br /> L'utilizzo di questa opzione può contribuire a ottimizzare l'allocazione di memoria, ma soltanto se la memoria fisica supera il limite configurato impostato dal sistema operativo per la memoria virtuale disponibile alle applicazioni. L'utilizzo di questa opzione può risultare appropriato in configurazioni con grandi quantità di memoria, in cui i requisiti di utilizzo della memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] risultano atipici e lo spazio degli indirizzi virtuali del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è completamente utilizzato. L'utilizzo errato di questa opzione può impedire l'avvio dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o generare errori di esecuzione.<br /><br /> Usare il valore predefinito per il parametro **-g** a meno che nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non venga visualizzato uno degli avvisi seguenti:<br /><br /> -"Non è stato possibile virtuale allocare byte: FAIL_VIRTUAL_RESERVE \<size>"<br /><br /> -"Non è stato possibile virtuale allocare byte: FAIL_VIRTUAL_COMMIT \<size>"<br /><br /> Questi messaggi possono indicare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sta tentando di liberare settori del pool di memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'inserimento di elementi, ad esempio i file con estensione dll delle stored procedure estese o gli oggetti di automazione. In questo caso, è consigliabile aumentare la quantità di memoria riservata usando l'opzione **-g** .<br /><br /> L'utilizzo di un valore minore di quello predefinito aumenta la quantità di memoria disponibile per il pool di memoria gestito da Gestione memoria e dagli stack di thread di SQL Server, offrendo alcuni vantaggi in termini di prestazioni per carichi di lavoro a utilizzo elevato di memoria in sistemi che non utilizzano un gran numero di stored procedure estese, query distribuite o oggetti di automazione.|  
|**-m**|Avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo. Quando si avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo, la connessione è consentita a un solo utente e il processo CHECKPOINT non viene avviato. CHECKPOINT assicura la regolare scrittura delle transazioni completate dalla cache del disco al database. Questa opzione viene in genere utilizzata per la risoluzione di problemi che richiedono interventi nei database di sistema Abilita l'opzione sp_configure allow updates. Per impostazione predefinita, l'opzione allow updates è disabilitata. L'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo consente a qualsiasi membro del gruppo Administrators locale del computer di connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come membro del ruolo predefinito del server sysadmin. Per altre informazioni, vedere [Connettersi a SQL Server se gli amministratori di sistema sono bloccati](connect-to-sql-server-when-system-administrators-are-locked-out.md). Per altre informazioni sulla modalità utente singolo, vedere [Avvio di SQL Server in modalità utente singolo](start-sql-server-in-single-user-mode.md).|  
|**-m "Nome applicazione Client"**|Quando si usa l'opzione **-m** con **SQLCMD** o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], l'opzione limita le connessioni a un'applicazione client specificata. Ad esempio, **-m"SQLCMD"** limita le connessioni a una singola connessione che deve identificarsi come programma client **SQLCMD**. Utilizzare questa opzione quando si avvia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo e un'applicazione client sconosciuta accede all'unica connessione disponibile. Per connettersi con l'editor di query in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], usare **-m"Microsoft SQL Server Management Studio - Query"** .<br /><br /> Al nome dell'applicazione client viene applicata la distinzione maiuscole/minuscole.<br /><br /> **\*\* Nota di sicurezza \*\*** Non usare questa opzione come caratteristica di sicurezza. L'applicazione client fornisce il nome dell'applicazione client stessa e può indicare un nome falso come parte della stringa di connessione.|  
|**-n**|Disattiva l'utilizzo del registro applicazioni di Windows per la registrazione degli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene avviata con **-n**, è consigliabile usare anche l'opzione di avvio **-e** . In caso contrario, gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non verranno registrati.|  
|**-s**|Avvia un'istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se il parametro **-s** non è impostato, verrà eseguito un tentativo di avviare l'istanza predefinita. Al prompt dei comandi è necessario passare alla directory BINN appropriata per l'istanza prima di avviare **sqlservr.exe**. Ad esempio, se Instance1 usa \mssql$Instance1 per i relativi file binari, l'utente deve passare alla directory \mssql$Instance1\binn per avviare **sqlservr.exe -s instance1**.|  
|**-T**  *trace#*|Indica l'avvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con uno specifico flag di traccia (*trace#* ) attivo. I flag di traccia vengono utilizzati per avviare il server con un funzionamento non standard. Per altre informazioni, vedere [Flag di traccia &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).<br /><br /> **\*\* Importante \*\*** Quando si specifica un flag di traccia con l'opzione **-T** , usare una lettera "T" maiuscola per passare il numero del flag di traccia. La lettera "t" minuscola è accettata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma imposta altri flag di traccia interni necessari solo ai tecnici del supporto tecnico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I parametri specificati nella finestra di avvio del Pannello di controllo non vengono letti.|  
|**-x**|Disabilita le caratteristiche di monitoraggio seguenti:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Contatori di Performance Monitor<br /><br /> Registrazione di statistiche relative al tempo di CPU e alla frequenza di accesso alla cache<br /><br /> Raccolta di informazioni per il comando DBCC SQLPERF<br /><br /> Raccolta di informazioni per alcune viste a gestione dinamica<br /><br /> Molti punti evento di eventi estesi<br /><br /> <br /><br /> **\*\* Avviso \* \***  quando si usa il **- x** opzione di avvio, le informazioni disponibili per la diagnosi delle prestazioni e problemi funzionali relativi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono notevolmente ridotte.|  
|**-E**|Aumenta il numero di extent allocati per ogni file in un filegroup. Questa opzione può risultare utile per applicazioni del data warehouse per cui il numero di utenti che eseguono analisi dell'indice o dei dati è limitato. Si consiglia di non utilizzarla in altre applicazioni poiché potrebbe influire negativamente sulle prestazioni. Tale opzione non è supportata nelle versioni a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="using-startup-options-for-troubleshooting"></a>Utilizzo delle opzioni di avvio per la risoluzione dei problemi  
 Alcune opzioni di avvio, ad esempio la modalità utente singolo e con configurazione minima, vengono utilizzate principalmente per la risoluzione dei problemi. L'avvio del server con l'opzione **-m** o **-f** per la risoluzione dei problemi risulta più semplice dalla riga di comando durante l'avvio manuale di sqlservr.exe.  
  
> [!NOTE]  
>  Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene avviato usando **net start**, le opzioni di avvio usano una barra (/) anziché un trattino (-).  
  
## <a name="using-startup-options-during-normal-operations"></a>Utilizzo delle opzioni di avvio durante il funzionamento normale  
 Può essere necessario utilizzare particolari opzioni a ogni avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'impostazione di queste opzioni, ad esempio **-g** o l'avvio con un flag di traccia, è più semplice se si configurano i parametri di avvio con Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questi strumenti consentono di salvare le opzioni di avvio come chiavi del Registro di sistema e di avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre con le opzioni di avvio.  
  
## <a name="compatibility-support"></a>Informazioni sulla compatibilità  
 Il parametro **-h**  non è supportato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Questo parametro è stato utilizzato in versioni precedenti di istanze a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per riservare spazio di indirizzi della memoria virtuale per metadati della memoria a caldo quando AWE è abilitato. Per altre informazioni, vedere [Funzionalità di SQL Server obsolete in SQL Server 2014](../../getting-started/discontinued-sql-server-features-in-sql-server-2014.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 [Configurare l'opzione di configurazione del server scan for startup procs](configure-the-scan-for-startup-procs-server-configuration-option.md)  
  
 [Avviare, arrestare, sospendere, riprendere, riavviare il motore di database, SQL Server Agent o SQL Server Browser](start-stop-pause-resume-restart-sql-server-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [CHECKPOINT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/checkpoint-transact-sql)   
 [Applicazione sqlservr](../../tools/sqlservr-application.md)  
  
  
