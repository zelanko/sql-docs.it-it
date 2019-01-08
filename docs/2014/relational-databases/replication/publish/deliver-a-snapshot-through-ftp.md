---
title: Recapitare uno snapshot tramite FTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2e3422e1fc41069bcb1f5f88c841212b5415cacd
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777563"
---
# <a name="deliver-a-snapshot-through-ftp"></a>Recapito di snapshot tramite FTP
  In questo argomento viene descritto come recapitare uno snapshot utilizzando l'FTP in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Prerequisiti](#Prerequisites)  
  
     [Sicurezza](#Security)  
  
-   **Per recapitare uno snapshot tramite FTP, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   L'agente snapshot deve disporre delle autorizzazioni di scrittura per la directory specificata, mentre l'agente di distribuzione o l'agente di merge deve disporre delle autorizzazioni di lettura. Se vengono usate sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\serverftp\home\snapshot. Per altre informazioni, vedere [Proteggere la cartella snapshot](../security/secure-the-snapshot-folder.md).  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   Prima di trasferire file snapshot tramite il protocollo FTP (File Transfer Protocol), è necessario configurare un server FTP. Per ulteriori informazioni, vedere la documentazione di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS).  
  
###  <a name="Security"></a> Sicurezza  
 Per migliorare la sicurezza, si consiglia di implementare una rete privata virtuale (VPN) quando si utilizza il recapito di snapshot tramite FTP in Internet. Per altre informazioni, vedere [Pubblicare i dati su Internet tramite VPN](../publish-data-over-the-internet-using-vpn.md).  
  
 Ai fini della sicurezza è consigliabile non consentire accessi anonimi al server FTP. L'agente snapshot deve disporre delle autorizzazioni di scrittura per la directory specificata, mentre l'agente di distribuzione o l'agente di merge deve disporre delle autorizzazioni di lettura. Se vengono usate sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\serverftp\home\snapshot. Per altre informazioni, vedere [Proteggere la cartella snapshot](../security/secure-the-snapshot-folder.md).  
  
 Se possibile, richiedere agli utenti di immettere le credenziali in fase di esecuzione. Se si archiviano le credenziali in un file script, è necessario proteggere il file.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Dopo la configurazione del server FTP specificare la directory e le informazioni di sicurezza relative a questo server nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**. Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-ftp-information"></a>Per specificare informazioni FTP  
  
1.  Nella finestra di dialogo **Proprietà pubblicazione - \<Publication>** selezionare **I Sottoscrittori possono scaricare i file di snapshot utilizzando FTP (File Transfer Protocol)** da una delle pagine seguenti:  
  
    -   La pagina **Snapshot FTP** , per le pubblicazioni di snapshot e transazionali e le pubblicazioni di tipo merge per i server di pubblicazione in cui sono in esecuzione versioni precedenti a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
    -   La pagina **Snapshot FTP e Internet** , per le pubblicazioni di tipo merge provenienti dai server di pubblicazione in cui è in esecuzione [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o una versione successiva.  
  
2.  Specificare i valori per **Nome server FTP**, **Numero di porta**, **Percorso dalla cartella radice FTP**, **Nome account di accesso**e **Password**.  
  
     Ad esempio, se la radice del server FTP è \\\serverftp\home e si vogliono archiviare gli snapshot nel percorso \\\serverftp\home\snapshot, specificare \snapshot\ftp per la proprietà **Percorso dalla cartella radice FTP**. La replica aggiunge "ftp" al percorso della cartella snapshot durante la creazione dei file di snapshot.  
  
3.  Specificare che tramite l'agente snapshot i file di snapshot devono essere scritti nella directory specificata al passaggio 2. Ad esempio, per fare in modo che l'agente snapshot scriva i file di snapshot in \\\serverftp\home\snapshot\ftp, è necessario specificare il percorso \\\serverftp\home\snapshot in una delle due posizioni indicate di seguito:  
  
    -   Il percorso predefinito dello snapshot per il server di distribuzione associato a questa pubblicazione.  
  
         Per altre informazioni sull'impostazione del percorso predefinito degli snapshot, vedere [Specificare la posizione predefinita degli snapshot &#40;SQL Server Management Studio&#41;](../specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
    -   Un percorso alternativo per la cartella snapshot per questa pubblicazione. Se lo snapshot è compresso viene richiesto un percorso alternativo.  
  
         Immettere il percorso nella casella di testo **Inserisci i file nella cartella seguente** nella pagina Snapshot della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**. Per ulteriori informazioni sui percorsi alternativi delle cartelle snapshot, vedere [Alternate Snapshot Folder Locations](../alternate-snapshot-folder-locations.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 È possibile impostare l'opzione per rendere i file snapshot disponibili in un server FTP e modificare le impostazioni FTP a livello di programmazione utilizzando stored procedure di replica. La stored procedure utilizzata varia a seconda del tipo di pubblicazione. Il recapito di snapshot tramite FTP viene utilizzato solo con le sottoscrizioni pull.  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-snapshot-or-transactional-publication"></a>Per abilitare il recapito di snapshot tramite FTP per una pubblicazione snapshot o transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Specificare **@publication**, un valore di `true` per **@enabled_for_internet**e valori appropriati per i parametri seguenti:  
  
    -   **@ftp_address** : indirizzo del server FTP utilizzato per il recapito dello snapshot.  
  
    -   (Facoltativo) **@ftp_port** : porta utilizzata dal server FTP.  
  
    -   (Facoltativo) **@ftp_subdirectory** : la sottodirectory della directory FTP predefinita assegnata a un account di accesso FTP. Ad esempio, se la radice del server FTP è \\\serverftp\home e si vogliono archiviare gli snapshot in \\\serverftp\home\snapshot, specificare **\snapshots\ftp** per **@ftp_subdirectory**. La replica aggiungerà "ftp" al percorso della cartella snapshot durante la creazione di file di snapshot.  
  
    -   (Facoltativo) **@ftp_login** : account di accesso utilizzato per la connessione al server FTP.  
  
    -   (Facoltativo) **@ftp_password** : password per l'accesso FTP.  
  
     Verrà creata una pubblicazione che utilizza FTP. Per altre informazioni, vedere [Create a Publication](create-a-publication.md).  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-merge-publication"></a>Per attivare il recapito di snapshot tramite FTP per una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Specificare **@publication**, un valore di `true` per **@enabled_for_internet** e valori appropriati per i parametri seguenti:  
  
    -   **@ftp_address** : indirizzo del server FTP utilizzato per il recapito dello snapshot.  
  
    -   (Facoltativo) **@ftp_port** : porta utilizzata dal server FTP.  
  
    -   (Facoltativo) **@ftp_subdirectory** : la sottodirectory della directory FTP predefinita assegnata a un account di accesso FTP. Ad esempio, se la radice del server FTP è \\\serverftp\home e si vogliono archiviare gli snapshot in \\\serverftp\home\snapshot, specificare **\snapshots\ftp** per **@ftp_subdirectory**. La replica aggiungerà "ftp" al percorso della cartella snapshot durante la creazione di file di snapshot.  
  
    -   (Facoltativo) **@ftp_login** : account di accesso utilizzato per la connessione al server FTP.  
  
    -   (Facoltativo) **@ftp_password** : password per l'accesso FTP.  
  
     Verrà creata una pubblicazione che utilizza FTP. Per altre informazioni, vedere [Create a Publication](create-a-publication.md).  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication-that-uses-ftp-snapshot-delivery"></a>Per creare una sottoscrizione pull in una pubblicazione snapshot o transazionale che utilizza il recapito di snapshot tramite FTP  
  
1.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Specificare **@publisher** e **@publication**.  
  
    -   Nel database di sottoscrizione del Sottoscrittore eseguire [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Specificare **@publisher**, **@publisher_db**, **@publication**, il [!INCLUDE[msCoName](../../../includes/msconame-md.md)] le credenziali di Windows con cui l'agente di distribuzione nel Sottoscrittore dura **@job_login** e **@job_password**e il valore `true` per **@use_ftp**.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) per registrare la sottoscrizione pull. Per altre informazioni, vedere [Creazione di una sottoscrizione pull](../create-a-pull-subscription.md).  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication-that-uses-ftp-snapshot-delivery"></a>Per creare una sottoscrizione pull in una pubblicazione di tipo merge che utilizza il recapito di snapshot tramite FTP  
  
1.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Specificare **@publisher** e **@publication**.  
  
2.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql). Specificare **@publisher**, **@publisher_db**, **@publication**, le credenziali di Windows con cui viene eseguito l'agente di distribuzione nel Sottoscrittore per **@job_login** e **@job_password**e il valore `true` per **@use_ftp**.  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql) per registrare la sottoscrizione pull. Per altre informazioni, vedere [Creazione di una sottoscrizione pull](../create-a-pull-subscription.md).  
  
#### <a name="to-change-one-or-more-ftp-snapshot-delivery-settings-for-a-snapshot-or-transactional-publication"></a>Per modificare una o più impostazioni del recapito di snapshot tramite FTP per una pubblicazione snapshot o transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Specificare uno dei valori seguenti per **@property** e un nuovo valore di questa impostazione per **@value**:  
  
    -   `ftp_address`: indirizzo del server FTP utilizzato per il recapito dello snapshot.  
  
    -   `ftp_port`: porta utilizzata dal server FTP.  
  
    -   `ftp_subdirectory`: sottodirectory della directory FTP predefinita utilizzata per lo snapshot tramite FTP.  
  
    -   `ftp_login`: account di accesso utilizzato per la connessione al server FTP.  
  
    -   `ftp_password`: password per l'account di accesso FTP.  
  
2.  (Facoltativo) Ripetere il passaggio 1 per ogni impostazione FTP da modificare.  
  
3.  (Facoltativo) Per disabilitare il recapito di snapshot tramite FTP, eseguire [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) nel database di pubblicazione del server di pubblicazione. Specificare il valore `enabled_for_internet` per **@property** e il valore `false` per **@value**.  
  
#### <a name="to-change-ftp-snapshot-delivery-settings-for-a-merge-publication"></a>Per modificare le impostazioni del recapito di snapshot tramite FTP per una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Specificare uno dei valori seguenti per **@property** e un nuovo valore di questa impostazione per **@value**:  
  
    -   `ftp_address`: indirizzo del server FTP utilizzato per il recapito dello snapshot.  
  
    -   `ftp_port`: porta utilizzata dal server FTP.  
  
    -   `ftp_subdirectory`: sottodirectory della directory FTP predefinita utilizzata per lo snapshot tramite FTP.  
  
    -   `ftp_login`: account di accesso utilizzato per la connessione al server FTP.  
  
    -   `ftp_password`: password per l'account di accesso FTP.  
  
2.  (Facoltativo) Ripetere il passaggio 1 per ogni impostazione FTP da modificare.  
  
3.  (Facoltativo) Per disabilitare il recapito di snapshot tramite FTP, eseguire [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) nel database di pubblicazione del server di pubblicazione. Specificare il valore `enabled_for_internet` per **@property** e il valore `false` per **@value**.  
  
###  <a name="TsqlExample"></a> Esempi (Transact-SQL)  
 Nell'esempio seguente viene creata una pubblicazione di tipo merge che consente ai Sottoscrittori di accedere ai dati dello snapshot tramite FTP. Il Sottoscrittore deve utilizzare una connessione VPN sicura per l'accesso alla condivisione FTP. I valori dell'account di accesso e della password vengono forniti tramite le variabili di scripting**sqlcmd** . Per altre informazioni, vedere [Usare sqlcmd con variabili di scripting](../../scripting/sqlcmd-use-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubftp.sql#sp_createmergepub_ftp)]  
  
 Nell'esempio seguente viene creata una sottoscrizione in una pubblicazione di tipo merge in cui il Sottoscrittore ottiene lo snapshot tramite FTP. Il Sottoscrittore deve utilizzare una connessione VPN sicura per l'accesso alla condivisione FTP. I valori dell'account di accesso e della password vengono forniti tramite le variabili di scripting**sqlcmd** . Per altre informazioni, vedere [Usare sqlcmd con variabili di scripting](../../scripting/sqlcmd-use-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsub_ftp)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsubagent_ftp)]  
  
## <a name="see-also"></a>Vedere anche  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Trasferire snapshot tramite FTP](../transfer-snapshots-through-ftp.md)   
 [Modificare le proprietà di pubblicazioni e articoli](change-publication-and-article-properties.md)   
 [Inizializzare una sottoscrizione con uno snapshot](../initialize-a-subscription-with-a-snapshot.md)  
  
  
