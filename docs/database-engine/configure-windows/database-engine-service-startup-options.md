---
title: Opzioni di avvio del servizio del motore di database | Microsoft Docs
ms.custom: ''
ms.date: 05/31/2019
ms.prod: sql
ms.prod_service: high-availability
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
- single-user mode [SQL Server], startup parameter
- overriding default startup parameters
- minimal configuration mode [SQL Server], startup parameter
- default startup parameters
- temporarily override default startup parameters [SQL Server]
- startup parameters [SQL Server]
- starting SQL Server, parameters
ms.assetid: d373298b-f6cf-458a-849d-7083ecb54ef5
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 25fb3df76c54042b81a92af3a6fa29706ab9faae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66767591"
---
# <a name="database-engine-service-startup-options"></a>Opzioni di avvio del servizio del motore di database

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Le opzioni di avvio consentono di designare determinati percorsi di file necessari in fase di avvio e di specificare alcune condizioni a livello di server. Per la maggior parte degli utenti non è necessario specificare opzioni di avvio a meno che non si debbano risolvere problemi del [!INCLUDE[ssDE](../../includes/ssde-md.md)] o si verifichi un problema insolito e si ricevano istruzioni dal servizio di supporto tecnico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di utilizzare l'opzione di avvio.  
  
> [!WARNING]  
>  L'utilizzo improprio di opzioni di avvio può influire sulle prestazioni del server e impedire l'esecuzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
>
>  Avviare SQL Server in Linux con l'utente "mssql" per evitare problemi di avvio futuri. Esempio: `sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]` 
  
## <a name="about-startup-options"></a>Informazioni sulle opzioni di avvio  
 Quando si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il programma di installazione scrive un set di opzioni di avvio predefinite nel Registro di sistema di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Tali opzioni consentono di specificare un file del database master, un file di log del database master o un file di log degli errori alternativo. Se [!INCLUDE[ssDE](../../includes/ssde-md.md)] non è in grado di individuare i file necessario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene avviato.  
  
 Le opzioni di avvio possono essere impostate utilizzando Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Configurazione delle opzioni di avvio del server &#40;Gestione di configurazione SQL Server&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
## <a name="list-of-startup-options"></a>Elenco delle opzioni di avvio  
### <a name="default-startup-options"></a>Opzioni di avvio predefinite  

|Opzioni|Descrizione|  
|-----------------------------|-----------------|  
|**-d**  *master_file_path*|Percorso completo del file del database master (in genere, C:\Programmi\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\master.mdf). Se non si imposta questa opzione, vengono utilizzati i parametri esistenti nel Registro di sistema.|  
|**-e**  *error_log_path*|Percorso completo del file di log degli errori, in genere C:\Programmi\Microsoft SQL Server\MSSQL.*n*\MSSQL\LOG\ERRORLOG). Se non si imposta questa opzione, vengono utilizzati i parametri esistenti nel Registro di sistema.|  
|**-l**  *master_log_path*|Percorso completo del file di log del database master (in genere C:\Programmi\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\mastlog.ldf). Se non si specifica questa opzione, vengono utilizzati i parametri esistenti nel Registro di sistema.|  
  
### <a name="other-startup-options"></a>Altre opzioni di avvio   

|Opzioni |Descrizione|   
|---------------------------|-----------------|  
|**-c**|Riduce i tempi necessari per l'avvio quando si avvia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal prompt dei comandi. Il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] viene in genere avviato come servizio chiamando Gestione controllo servizi. Considerato che [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] non viene avviato come servizio quando viene eseguito l'avvio dal prompt dei comandi, usare **-c** per ignorare questo passaggio.|  
|**-f**|Avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la configurazione minima. È utile nel caso in cui l'impostazione di un valore di configurazione, ad esempio un'allocazione eccessiva di memoria, abbia impedito l'avvio del server. L'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la configurazione minima comporta l'attivazione della modalità utente singolo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere la descrizione di **-m** di seguito.|  
|**-kDecimalNumber**| Questo parametro di avvio limita il numero di richieste I/O al secondo del checkpoint. **DecimalNumber** rappresenta la velocità del checkpoint in MB al secondo.  La modifica di questo valore può influire sulla velocità dell'esecuzione di backup o processi di ripristino, pertanto procedere con cautela. Per altre informazioni su questo parametro di avvio, vedere la correzione rapida in cui è stato introdotto il [parametro -k](https://support.microsoft.com/en-us/help/929240/fix-i-o-requests-that-are-generated-by-the-checkpoint-process-may-caus).| 
|**-m**|Avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo. Quando si avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo, la connessione è consentita a un solo utente e il processo CHECKPOINT non viene avviato. CHECKPOINT assicura la regolare scrittura delle transazioni completate dalla cache del disco al database. Questa opzione viene in genere utilizzata per la risoluzione di problemi che richiedono interventi nei database di sistema Abilita l'opzione sp_configure allow updates. Per impostazione predefinita, l'opzione allow updates è disabilitata. L'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo consente a qualsiasi membro del gruppo Administrators locale del computer di connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come membro del ruolo predefinito del server sysadmin. Per altre informazioni, vedere [Connettersi a SQL Server se gli amministratori di sistema sono bloccati](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md). Per altre informazioni sulla modalità utente singolo, vedere [Avvio di SQL Server in modalità utente singolo](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md).|  
|**-m nome dell'applicazione client**|Limita le connessioni a un'applicazione client specificata. Ad esempio, `-mSQLCMD`  limita le connessioni a una singola connessione, che deve identificarsi come programma client SQLCMD. Utilizzare questa opzione quando si avvia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo e un'applicazione client sconosciuta accede all'unica connessione disponibile. Usare `"Microsoft SQL Server Management Studio - Query"` per connettersi con l'editor di query SSMS. L'opzione dell'editor di query SSMS non può essere configurata tramite Gestione configurazione [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] perché include il trattino che è invece rifiutato dallo strumento.<br /><br /> Al nome dell'applicazione client viene applicata la distinzione maiuscole/minuscole. Sono necessarie le virgolette doppie se il nome dell'applicazione contiene spazi o caratteri speciali.<br /><br />**Esempi di avvio dalla riga di comando:**<br /><br />`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\sqlservr -s MSSQLSERVER -m"Microsoft SQL Server Management Studio - Query"` <br /><br />`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\sqlservr -s MSSQLSERVER -mSQLCMD` <br /><br /> **Nota sulla sicurezza:** Non utilizzare tale opzione come caratteristica di sicurezza. L'applicazione client fornisce il nome dell'applicazione client stessa e può indicare un nome falso come parte della stringa di connessione.|  
|**-n**|Disattiva l'utilizzo del registro applicazioni di Windows per la registrazione degli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene avviata con **-n**, è consigliabile usare anche l'opzione di avvio **-e** . In caso contrario, gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non verranno registrati.|  
|**-s**|Avvia un'istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se il parametro **-s** non è impostato, verrà eseguito un tentativo di avviare l'istanza predefinita. Al prompt dei comandi è necessario passare alla directory BINN appropriata per l'istanza prima di avviare **sqlservr.exe**. Ad esempio, se Instance1 usa `\mssql$Instance1` per i relativi file binari, l'utente deve passare alla directory `\mssql$Instance1\binn` per avviare **sqlservr.exe -s instance1**.|  
|**-T**  *trace#*|Indica l'avvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con uno specifico flag di traccia (*trace#* ) attivo. I flag di traccia vengono utilizzati per avviare il server con un funzionamento non standard. Per altre informazioni, vedere [Flag di traccia &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).<br /><br /> **Importante:** Quando si specifica un flag di traccia con l'opzione **-T**, utilizzare una lettera "T" maiuscola per passare il numero del flag di traccia. La lettera "t" minuscola è accettata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma imposta altri flag di traccia interni necessari solo ai tecnici del supporto tecnico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I parametri specificati nella finestra di avvio del Pannello di controllo non vengono letti.|  
|**-x**|Disabilita le caratteristiche di monitoraggio seguenti:<br /> - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Contatori di Performance Monitor<br /> - Registrazione di statistiche relative al tempo di utilizzo della CPU e alla frequenza di accesso alla cache<br /> - Raccolta di informazioni per il comando DBCC SQLPERF<br /> - Raccolta di informazioni per alcune viste a gestione dinamica<br /> - Numerosi punti evento di eventi estesi<br /><br /> **Avviso:** Quando si utilizza l'opzione di avvio **-x**, le informazioni disponibili per la diagnosi delle prestazioni e dei problemi funzionali relativi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono notevolmente ridotte.|  
|**-E**|Aumenta il numero di extent allocati per ogni file in un filegroup. Questa opzione può risultare utile per applicazioni del data warehouse per cui il numero di utenti che eseguono analisi dell'indice o dei dati è limitato. Si consiglia di non utilizzarla in altre applicazioni poiché potrebbe influire negativamente sulle prestazioni. Tale opzione non è supportata nelle versioni a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="using-startup-options-for-troubleshooting"></a>Utilizzo delle opzioni di avvio per la risoluzione dei problemi  
 Alcune opzioni di avvio, ad esempio la modalità utente singolo e con configurazione minima, vengono utilizzate principalmente per la risoluzione dei problemi. L'avvio del server con l'opzione **-m** o **-f** per la risoluzione dei problemi risulta più semplice dalla riga di comando durante l'avvio manuale di sqlservr.exe.  
  
> [!NOTE]  
>  Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene avviato usando **net start**, le opzioni di avvio usano una barra (/) anziché un trattino (-).  
  
## <a name="using-startup-options-during-normal-operations"></a>Utilizzo delle opzioni di avvio durante il funzionamento normale  
 Può essere necessario utilizzare particolari opzioni a ogni avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'impostazione di queste opzioni, ad esempio l'avvio con un flag di traccia, è più semplice se si configurano i parametri di avvio con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Questi strumenti consentono di salvare le opzioni di avvio come chiavi del Registro di sistema e di avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre con le opzioni di avvio.  
  
## <a name="compatibility-support"></a>Informazioni sulla compatibilità  
 Il parametro **-h**  non è supportato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Questo parametro è stato utilizzato in versioni precedenti di istanze a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per riservare spazio di indirizzi della memoria virtuale per metadati della memoria a caldo quando AWE è abilitato. Per ulteriori informazioni, vedere [Funzionalità di SQL Server obsolete in SQL Server 2016](https://msdn.microsoft.com/library/0678bfbc-5d3f-44f4-89c0-13e8e52404da).  
  
## <a name="related-tasks"></a>Attività correlate  
[Configurare l'opzione di configurazione del server scan for startup procs](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)  
[Avviare, arrestare, sospendere, riprendere, riavviare il motore di database, SQL Server Agent o SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)
[Configure Server Startup Options (Configurare le opzioni di avvio del server) &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)
  
## <a name="see-also"></a>Vedere anche  
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [Applicazione sqlservr](../../tools/sqlservr-application.md)  
  
  
