---
title: Installare SQL Server con l'opzione di archiviazione su condivisione file SMB | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 8b7810b2-637e-46a3-9fe1-d055898ba639
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3242f463e24322921b16a513c1b3a6905965b390
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62775334"
---
# <a name="install-sql-server-with-smb-fileshare-as-a-storage-option"></a>Installazione di SQL Server con l'opzione di archiviazione su condivisione file SMB
  A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] i database di sistema (Master, Model, MSDB e TempDB) e i database utente del [!INCLUDE[ssDE](../../includes/ssde-md.md)] possono essere installati con il file server SMB (Server Message Block) come opzione di archiviazione. Questa condizione è valida per le installazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autonome e per le installazioni del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Filestream non è attualmente supportato in una condivisione file SMB.  
  
## <a name="installation-considerations"></a>Considerazioni sull'installazione  
  
### <a name="smb-file-share-formats"></a>Formati di condivisione di file SMB:  
 Quando si specifica la condivisione file SMB, sono supportati i seguenti formati di percorso UNC (Universal Naming Convention) per database autonomi e dell'istanza del cluster di failover:  
  
-   \\\NomeServer\NomeCondivisione\  
  
-   \\\NomeServer\NomeCondivisione  
  
 Per ulteriori informazioni su Universal Naming Convention, vedere [UNC](https://go.microsoft.com/fwlink/?LinkId=245534) (https://go.microsoft.com/fwlink/?LinkId=245534).  
  
 Il percorso UNC del loopback (percorso UNC il cui nome del server è localhost, 127.0.0.1 o il nome del computer locale) non è supportato. In un caso speciale, non è supportato neanche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui viene utilizzato il cluster di file server ospitato nello stesso nodo eseguito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per evitare questa situazione, è consigliabile che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il cluster di file server vengano creati in cluster Windows separati.  
  
 I formati di percorso UNC riportati di seguito non sono supportati:  
  
-   Percorso del loopback, ad esempio \\\localhost\\..\ o \\\127.0.0.1\\...\  
  
-   Condivisioni amministrative, ad esempio \\\nomeserver\x$  
  
-   Altri formati di percorso UNC come \\\\?\x:\  
  
-   Unità di rete su cui è stato eseguito il mapping  
  
### <a name="supported-data-definition-language-ddl-statements"></a>Istruzioni DDL (Data Definition Language) supportate  
 Le istruzioni DDL di [!INCLUDE[tsql](../../includes/tsql-md.md)] e le stored procedure del motore di database seguenti supportano le condivisioni file SMB:  
  
1.  [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
2.  [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
3.  [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
4.  [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)  
  
5.  [sp_attach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-db-transact-sql)  
  
6.  [sp_attach_single_file_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql)  
  
### <a name="installation-options"></a>Opzione di installazione  
  
-   Nella scheda "Directory dati" della pagina "Configurazione del motore di database" del programma di installazione, impostare il parametro "Directory radice dati" su "\\\fileserver1\share1\".  
  
-   Nell'installazione del prompt dei comandi, specificare "/INSTALLSQLDATADIR" come "\\\fileserver1\share1\".  
  
     Di seguito è riportata la sintassi di esempio per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un server autonomo utilizzando l'opzione di condivisione file SMB:  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="<StrongPassword>" /INSTALLSQLDATADIR="\\FileServer\Share1\" /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     Per installare un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a nodo singolo con il [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)](istanza predefinita):  
  
    ```  
    setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="\\FileServer\Share1\" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     Per ulteriori informazioni sull'utilizzo di diverse opzioni dei parametri della riga di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]comando in, vedere [Install SQL Server 2014 dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
## <a name="operating-system-considerations-smb-protocol-vs-includessnoversionincludesssnoversion-mdmd"></a>Considerazioni relative al sistema operativo (protocollo SMB e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])  
 Sistemi operativi Windows diversi dispongono di versioni diverse del protocollo SMB e la versione del protocollo SMB è trasparente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile individuare i vantaggi delle varie versioni del protocollo SMB in relazione a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Sistema operativo|Versione del protocollo SMB2|Vantaggi per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|----------------------|---------------------------|-------------------------------------------|  
|
  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP 2|2.0|Prestazioni migliorate rispetto a versioni precedenti di SMB.<br /><br /> Durabilità, che consente il recupero da problemi di rete temporanei.|  
|
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1, incluso Server Core|2.1|Supporto per MTU di grandi dimensioni che consente il trasferimento di grandi quantità di dati, ad esempio per le operazioni di backup e di ripristino di SQL. Questa funzionalità deve essere abilitata dall'utente. Per ulteriori informazioni su come abilitare questa funzionalità, vedere Novità [di SMB](https://go.microsoft.com/fwlink/?LinkID=237319) (https://go.microsoft.com/fwlink/?LinkID=237319).<br /><br /> Significativi miglioramenti nelle prestazioni, in particolare per i carichi di lavoro di tipo OLTP di SQL. Questi miglioramenti delle prestazioni richiedono l'applicazione di un hotfix. Per ulteriori informazioni sull'hotfix [, vedere la](https://go.microsoft.com/fwlink/?LinkId=237320) pagina relativahttps://go.microsoft.com/fwlink/?LinkId=237320)a.|  
|
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)], incluso Server Core|3.0|Supporto per il failover trasparente delle condivisioni file che garantisce tempi di inattività ridotti a zero senza interventi dell'amministratore del DBA SQL o del file server nelle configurazioni di cluster di file server.<br /><br /> Supporto per IO che utilizzano più interfacce di rete simultaneamente e tolleranza agli errori dell'interfaccia di rete.<br /><br /> Supporto per interfacce di rete con funzionalità RDMA.<br /><br /> Per ulteriori informazioni su queste funzionalità e su Server Message Block, vedere [Panoramica di Server Message Block](https://go.microsoft.com/fwlink/?LinkId=253174) (https://go.microsoft.com/fwlink/?LinkId=253174).<br /><br /> Supporto per File server di scalabilità orizzontale (SoFS) con disponibilità continua.|  
|
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2, incluso Server Core|3.2|Supporto per il failover trasparente delle condivisioni file che garantisce tempi di inattività ridotti a zero senza interventi dell'amministratore del DBA SQL o del file server nelle configurazioni di cluster di file server.<br /><br /> Supporto per IO che utilizzano più interfacce di rete simultaneamente e tolleranza agli errori dell'interfaccia di rete tramite SMB multicanale.<br /><br /> Supporto per interfacce di rete con funzionalità RDMA tramite SMB diretto.<br /><br /> Per ulteriori informazioni su queste funzionalità e su Server Message Block, vedere [Panoramica di Server Message Block](https://go.microsoft.com/fwlink/?LinkId=253174) (https://go.microsoft.com/fwlink/?LinkId=253174).<br /><br /> Supporto per File server di scalabilità orizzontale (SoFS) con disponibilità continua.<br /><br /> Ottimizzato per piccole operazioni I/O di lettura/scrittura casuali comuni per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLTP.<br /><br /> L'unità massima di trasmissione (MTU) è abilitata per impostazione predefinita per migliorare significativamente le prestazioni nei trasferimenti sequenziali di grandi dimensioni come il ripristino o il backup del database e il data warehouse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
## <a name="security-considerations"></a>Considerazioni relative alla sicurezza  
  
-   Gli account dei servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent devono disporre di autorizzazioni di condivisione di controllo completo e di autorizzazioni NTFS sulle cartelle condivise SMB. L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere un account di dominio o di sistema quando si utilizza un file server SMB. Per ulteriori informazioni sulle autorizzazioni di condivisione e NTFS, vedere la pagina relativa alle [autorizzazioni di condivisione e NTFS in un file server](https://go.microsoft.com/fwlink/?LinkId=245535) (https://go.microsoft.com/fwlink/?LinkId=245535).  
  
    > [!NOTE]  
    >  Le autorizzazioni di condivisione Controllo completo e le autorizzazioni NTFS sulle cartelle condivise SMB devono essere limitate a: account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e utenti di Windows con ruoli di amministratore del server.  
  
     Si consiglia per utilizzare un account di dominio come account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se l'account di sistema viene usato come account del servizio, concedere le autorizzazioni per l'account del computer nel formato: _<domain_name>_ **\\** _<computer_name>_ **$**.  
  
    > [!NOTE]  
    >  -   Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario specificare l'account di dominio come account del servizio se la condivisione file SMB viene specificata come opzione di archiviazione. Con le condivisioni file SMB, è possibile specificare l'account di sistema come account del servizio solo dopo l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
    > -   Gli account virtuali non possono essere autenticati a un percorso remoto. Per tutti gli account virtuali viene usata l'autorizzazione dell'account del computer. Eseguire il provisioning dell'account del computer nel formato _<domain_name>_ **\\** _<computer_name>_ **$**.  
  
-   L'account utilizzato per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve disporre di autorizzazioni FULL CONTROL sulla cartella della condivisione file SMB utilizzata come directory dei dati o su qualsiasi altra cartella dei dati (directory del database utente, directory del log del database utente, directory TempDB, directory del log TempDB, directory di backup) durante l'Installazione del cluster.  
  
-   È necessario che all'account utilizzato per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] venga concesso il privilegio SeSecurityPrivilege nel file server SMB. Per concedere tale privilegio, utilizzare la console Criteri di sicurezza locale nel file server per aggiungere l'account di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ai criteri Gestione file registro di controllo e di sicurezza. Questa impostazione è disponibile nella sezione Assegnazione diritti utente in Criteri locali nella console Criteri di sicurezza locale.  
  
## <a name="known-issues"></a>Problemi noti  
  
-   Dopo aver scollegato un database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] che si trova in un archivio collegato alla rete, è possibile che si verifichino problemi di autorizzazione del database durante il tentativo di ricollegare il database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il problema è definito in [questo articolo](https://go.microsoft.com/fwlink/?LinkId=237321) della Knowledgehttps://go.microsoft.com/fwlink/?LinkId=237321)parte (. Per evitarlo, vedere la sezione relativa a **ulteriori informazioni** nell'articolo della Knowledge Base.  
  
-   Alcune terze parti, ad esempio i dispositivi NetApp, non supportano tutte le chiamate all'API di SQL Server. Con questi si potrebbero ottenere:   
    2015-06-04 13:14:19.97 spid9s errore: 17053, gravità: 16, stato: 1.  
    2015-06-04 13:14:19.97 spid9s DoDevIoCtlOut () GetOverlappedResult (): errore del sistema operativo 1 (funzione non corretta.) rilevato.  
  
     Per NTFS, questo errore non provoca problemi,  ma per ReFS può provocare una riduzione significativa delle prestazioni.  
  
-   Se la condivisione file SMB viene utilizzata come opzione di archiviazione per un'istanza cluster di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per impostazione predefinita il log di diagnostica del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può essere scritto nella condivisione file perché la DLL risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non dispone di autorizzazioni di lettura/scrittura in una condivisione file. Per risolvere il problema, tentare uno dei metodi seguenti:  
  
    1.  Concedere autorizzazioni di lettura/scrittura in una condivisione file a tutti gli oggetti computer del cluster.  
  
    2.  Impostare il percorso dei log di diagnostica su un percorso file locale. Vedere l'esempio seguente:  
  
        ```sql  
        ALTER SERVER CONFIGURATION  
        SET DIAGNOSTICS LOG PATH = 'C:\logs';  
        ```  
  
## <a name="see-also"></a>Vedere anche  
 [Pianificazione di un'installazione di SQL Server](../../../2014/sql-server/install/planning-a-sql-server-installation.md)   
 [Procedure per l'installazione](../../../2014/sql-server/install/installation-how-to-topics.md)   
 [Configurare account di servizio e autorizzazioni di Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
