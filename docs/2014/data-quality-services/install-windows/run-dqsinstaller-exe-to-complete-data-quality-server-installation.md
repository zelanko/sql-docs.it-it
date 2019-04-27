---
title: Eseguire DQSInstaller.exe per completare l'installazione del server DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7a8c96e0-1328-4f35-97fc-b6d9cb808bae
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a47a205ca7d216f17ec8a5893483180235b775a5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62792502"
---
# <a name="run-dqsinstallerexe-to-complete-data-quality-server-installation"></a>Eseguire DQSInstaller.exe per completare l'installazione del server DQS
  Per completare l'installazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , è necessario eseguire il file DQSInstaller.exe dopo l'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Questo argomento descrive come eseguire DQSInstaller.exe dalla schermata **Start** , dal menu **Start** , da Esplora risorse o dal prompt dei comandi. Per eseguire il file DQSInstaller.exe è possibile scegliere una qualsiasi delle modalità.  
  
##  <a name="Prerequisites"></a> Prerequisiti  
  
-   È necessario aver selezionato **Data Quality Services** in **Servizi motore di database** nella pagina Selezione funzionalità del programma di installazione di SQL Server e aver completato l'installazione di SQL Server. Per altre informazioni, vedere [Installare Data Quality Services](install-data-quality-services.md).  
  
-   È necessario che l'account utente di Windows sia membro del ruolo predefinito del server sysadmin nell'istanza del motore di database di SQL Server.  
  
-   È necessario aver eseguito l'accesso come membro del gruppo di amministratori sul computer in cui viene eseguito DQSInstaller.exe.  
  
##  <a name="WindowsExplorer"></a> Eseguire DQSInstaller.exe dalla schermata Start, dal menu Start o da Esplora risorse  
  
1.  Nel computer in cui si è scelto di installare [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]eseguire il file DQSInstaller.exe tramite una delle modalità seguenti, in base al contesto appropriato:  
  
    -   **Schermata Start**: nella schermata **Start** fare clic su **Programma di installazione di Data Quality Server**.  
  
    -   **Menu Start**: Nella barra delle applicazioni, fare clic su **avviare**, scegliere **tutti i programmi**, fare clic su **Microsoft SQL Server 2014**. Sotto **Microsoft SQL Server 2014**, fare clic su **Data Quality Services**, quindi fare clic su **il programma di installazione di Data Quality Server.**  
  
    -   **Esplora risorse**: Individuare il file DQSInstaller.exe. Se è stata installata l'istanza predefinita di SQL Server, il file DQSinstaller.exe sarà disponibile in C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn. Fare doppio clic sul file DQSInstaller.exe.  
  
2.  Verrà visualizzata una finestra del prompt dei comandi in cui viene indicato lo stato dell'installazione. Si noterà quanto segue:  
  
    1.  Tramite il programma di installazione viene creato un file di log dell'installazione, DQS_install.log, contenente informazioni sulle azioni effettuate durante l'esecuzione del file DQSInstaller.exe. Se è stata installata l'istanza predefinita di SQL Server, il file DQS_install.log sarà disponibile in C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log.  
  
    2.  Per l'installazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]vengono utilizzate le regole di confronto del server predefinite, SQL_Latin1_General_CP1_CI_AS.  
  
        > [!IMPORTANT]  
        >  È possibile fornire un valore delle regole di confronto di un altro server per l'installazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] solo se si esegue DQSInstaller.exe dal prompt dei comandi. Per altre informazioni, vedere [Eseguire DQSInstaller.exe dal prompt dei comandi](#CommandPrompt) più avanti in questo argomento.  
  
    3.  Il programma di installazione consente di verificare tutti i riavvii in sospeso nel computer dovuti ad aggiornamenti eseguiti di recente. Se si rilevano riavvii in sospeso, verrà visualizzato un apposito messaggio. È possibile scegliere di continuare o di interrompere l'installazione premendo rispettivamente Sì o No. In tal caso, è necessario interrompere l'installazione, riavviare il computer, quindi eseguire nuovamente il file DQSInstaller.exe.  
  
3.  Viene richiesto di digitare una password per la chiave master del database. Questa chiave è necessaria per crittografare le chiavi del provider di servizio dati di riferimento che saranno archiviate nel database DQS_MAIN quando i provider di dati di riferimento vengono configurati in [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) in un secondo momento.  
  
    > [!IMPORTANT]  
    >  La password deve essere composta da almeno 8 caratteri e deve contenere caratteri di tre delle quattro categorie seguenti: una lettera maiuscola (A, B, C,... Z), una lettera minuscola (a, b, c,... z), un numero (0, 1, 2,... 9) e un carattere speciale o non alfanumerico (~!@#$%^&*()_-+=|\\{}[]:;"'<>,.?/). Ad esempio: P@ssword. Tramite il programma di installazione verrà richiesto di immettere un'altra password se quella corrente non soddisfa il requisito.  
  
4.  Immettere una password, confermarla, quindi premere INVIO per continuare l'installazione.  
  
    > [!IMPORTANT]  
    >  È necessario conservare la password specificata per la chiave master del database perché verrà richiesta per il ripristino dei database DQS da un backup, se si sceglie di eseguire questa azione. Per altre informazioni sul ripristino dei database DQS, vedere [Backup e ripristino di database DQS](../backing-up-and-restoring-dqs-databases.md).  
  
5.  Se un database Master Data Services è presente nella stessa istanza di SQL Server come [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], viene creato un utente di cui è stato eseguito il mapping all'account di accesso a Master Data Services e a cui viene concesso il ruolo dqs_administrator nel database DQS_MAIN. Per informazioni sull'installazione di Master Data Services e sulla creazione di un database Master Data Services, vedere [Installare Master Data Services](../../master-data-services/install-windows/install-master-data-services.md).  
  
6.  Dopo che l'installazione è stata completata correttamente verrà visualizzato un messaggio di completamento. Premere un tasto qualsiasi per chiudere la finestra del prompt dei comandi.  
  
##  <a name="CommandPrompt"></a> Eseguire DQSInstaller.exe dal prompt dei comandi  
 È possibile eseguire il file DQSInstaller.exe dal prompt dei comandi utilizzando i parametri della riga di comando riportati di seguito:  
  
|Parametro di DQSInstaller.exe|Descrizione|Sintassi di esempio|  
|--------------------------------|-----------------|-------------------|  
|-collation|Regole di confronto del server da utilizzare per l'installazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].<br /><br /> DQS supporta solo le regole di confronto senza distinzione tra maiuscole e minuscole. Se si specificano regole di confronto con distinzione tra maiuscole e minuscole, tramite il programma di installazione si tenterà di utilizzare la versione senza distinzione tra maiuscole e minuscole delle regole di confronto specificate. Se non è disponibile alcuna versione senza distinzione tra maiuscole e minuscole o se le regole di confronto non sono supportate da SQL, l'installazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] non verrà completata.<br /><br /> Se non vengono specificate regole di confronto del server, vengono utilizzate quelle predefinite, cioè SQL_Latin1_General_CP1_CI_AS.|`dqsinstaller.exe -collation <collation_name>`|  
|-upgradedlls|Viene ignorata la ricreazione dei database DQS (DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA) e vengono aggiornati solo gli assembly SQLCLR (SQL Common Language Runtime) utilizzati da DQS nel database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .<br /><br /> Per altre informazioni, vedere [Aggiornare gli assembly SQLCLR dopo l'aggiornamento di .NET Framework](upgrade-sqlclr-assemblies-after-net-framework-update.md)|`dqsinstaller.exe -upgradedlls`|  
|-exportkbs|Esportare tutte le Knowledge Base in un file di backup DQS (con estensione dqsb). È inoltre necessario specificare il percorso completo e il nome file in cui si desidera esportare tutte le Knowledge Base.<br /><br /> Per altre informazioni, vedere [Esportare e importare le Knowledge Base di DQS con DQSInstaller.exe](export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md).|`dqsinstaller.exe -exportkbs <path><filename>`<br /><br /> Ad esempio, `dqsinstaller.exe -exportkbs c:\DQSBackup.dqsb`|  
|-importkbs|Importare tutte le Knowledge Base da un file di backup DQS (con estensione dqsb) dopo aver completato l'installazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . È inoltre necessario specificare il percorso completo e il nome file da cui si desidera importare tutte le Knowledge Base.<br /><br /> Per altre informazioni, vedere [Esportare e importare le Knowledge Base di DQS utilizzando DQSInstaller.exe](export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md).|`dqsinstaller.exe -importkbs <path><filename>`<br /><br /> Ad esempio, `dqsinstaller.exe -importkbs c:\DQSBackup.dqsb`|  
|-upgrade|Aggiorna lo schema dei database DQS. Questo parametro deve essere utilizzato dopo aver installato un aggiornamento di SQL Server in un'istanza di DQS configurata in precedenza. Per altre informazioni, vedere [Aggiornare lo schema dei database DQS dopo l'installazione dell'aggiornamento di SQL Server](upgrade-dqs-databases-schema-after-installing-sql-server-update.md).|`dqsinstaller.exe -upgrade`|  
|-uninstall|Disinstalla [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] dall'istanza di SQL Server corrente.<br /><br /> È inoltre possibile esportare tutte le Knowledge Base dell'installazione esistente di Data Quality Server in un file di backup DQS (con estensione dqsb) e successivamente disinstallare Data Quality Server. Per altre informazioni, vedere [Esportare e importare le Knowledge Base di DQS utilizzando DQSInstaller.exe](export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md).<br /><br /> **\*\* Importante \*\*** Se si disinstalla [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] da un'istanza di SQL Server usando il parametro della riga di comando `-uninstall` , tutti gli oggetti DQS vengono eliminati nell'ambito del processo di disinstallazione. Non è necessario eliminarli manualmente dopo la disinstallazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] come indicato in [Rimuovere oggetti server Data Quality Services](../../sql-server/install/remove-data-quality-server-objects.md).|**Per disinstallare solo Data Quality Server:** <br /> `dqsinstaller.exe -uninstall`<br /><br /> **Per esportare tutte le Knowledge Base in un file e successivamente disinstallare Data Quality Server:** <br /> `dqsinstaller.exe -uninstall <path><filename>` <br />Ad esempio, `dqsinstaller.exe -uninstall c:\DQSBackup.dqsb`|  
  
 **Per eseguire DQSInstaller.exe dal prompt dei comandi:**  
  
1.  Avviare il prompt dei comandi.  
  
2.  Al prompt dei comandi impostare la directory sul percorso in cui è disponibile il file DQSInstaller.exe. Se è stata installata l'istanza predefinita di SQL Server, il file DQSinstaller.exe sarà disponibile in C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn:  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  Al prompt dei comandi, eseguire DQSInstaller.exe con o senza parametri della riga di comando:  
  
    -   **Senza parametro della riga di comando**: Digitare `dqsinstaller.exe` e quindi premere INVIO.  
  
    -   **Con parametro della riga di comando**: Digitare il comando obbligatorio come indicato nella tabella precedente e quindi premere INVIO.  
  
4.  Le azioni obbligatorie vengono eseguite in base al comando specificato. Se si è scelto di installare [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] senza parametri della riga di comando, i passaggi restanti sono uguali a quelli indicati da 2 a 6 nella precedente sezione [Eseguire DQSInstaller.exe dalla schermata Start, dal menu Start o da Esplora risorse](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer).  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   Concedere ruoli DQS appropriati agli utenti in base al relativo profilo di lavoro. Vedere [Concedere ruoli DQS agli utenti](grant-dqs-roles-to-users.md).  
  
-   Se l'accesso a [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] verrà eseguito in modalità remota da [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)], abilitare il protocollo TCP/IP utilizzando Gestione configurazione SQL Server nel computer.  
  
-   Assicurarsi che sia possibile accedere ai dati di origine per le operazioni DQS e di poter esportare i dati elaborati in una tabella di un database. Vedere [Accedere ai dati per le operazioni DQS](access-data-for-the-dqs-operations.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Installare Data Quality Services](install-data-quality-services.md)   
 [Aggiornare gli assembly SQLCLR dopo l'aggiornamento di .NET Framework](upgrade-sqlclr-assemblies-after-net-framework-update.md)   
 [Esportare e importare le Knowledge Base di DQS con DQSInstaller.exe](export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)  
  
  
