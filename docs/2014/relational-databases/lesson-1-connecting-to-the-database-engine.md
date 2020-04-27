---
title: 'Lezione 1: Connessione al motore di database | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e8db82f0-50ed-4531-9209-940006ed34cb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 32b78c210647ab5b3722f01f334e9cb2e8bbfc13
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63145478"
---
# <a name="lesson-1-connecting-to-the-database-engine"></a>Lezione 1: Connessione al Motore di database
  Gli strumenti che vengono installati con [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]dipendono dall'edizione in uso e dalle opzioni di installazione selezionate. In questa lezione vengono illustrati gli strumenti principali e vengono descritte le procedure per la connessione e l'esecuzione di una funzione di base, ovvero la concessione di autorizzazione ad altri utenti.  
  
  
  
##  <a name="tools-for-getting-started"></a><a name="tools"></a>Strumenti per Introduzione  
 In [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] è disponibile un'ampia gamma di strumenti. In questo argomento vengono illustrati i primi strumenti necessari e vengono fornite indicazioni utili per selezionare lo strumento appropriato per le operazioni da eseguire. A tutti gli strumenti è possibile accedere dal menu **Start** . Alcuni strumenti, quali [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], non vengono installati per impostazione predefinita. ma devono essere selezionati tra i componenti client durante l'installazione. Per una descrizione completa degli strumenti illustrati di seguito, eseguire una ricerca nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] contiene solo un subset degli strumenti.  
  
### <a name="basic-tools"></a>Strumenti di base  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] è lo strumento principale per l'amministrazione di [!INCLUDE[ssDE](../includes/ssde-md.md)] e la scrittura di codice [!INCLUDE[tsql](../includes/tsql-md.md)]. È ospitato nella shell di [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] . Non è incluso in [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] , ma è disponibile come download separato dall' [area download Microsoft](https://go.microsoft.com/fwlink/?LinkId=144346).  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Gestione configurazione viene installato sia con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che con gli strumenti client. Consente di abilitare protocolli server, configurare le opzioni relative ai protocolli quali le porte TCP, configurare i servizi server per l'avvio automatico e configurare i computer client per la connessione con le modalità preferite. Questo strumento consente di configurare gli elementi di connettività più avanzati ma non le funzionalità.  
  
### <a name="sample-database"></a>Database di esempio  
 I database di esempio e gli esempi non sono inclusi in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Nella maggior parte degli esempi descritti nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene usato il database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] .  
  
##### <a name="to-start-sql-server-management-studio"></a>Per avviare SQL Server Management Studio  
  
-   Dal menu **Start** scegliere **tutti i programmi**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]e quindi fare clic su **SQL Server Management Studio**.  
  
##### <a name="to-start-sql-server-configuration-manager"></a>Per avviare Gestione configurazione SQL Server  
  
-   Fare clic sul menu **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
##  <a name="connecting-with-management-studio"></a><a name="connect"></a>Connessione con Management Studio  
 La connessione a [!INCLUDE[ssDE](../includes/ssde-md.md)] dagli strumenti in esecuzione nello stesso computer risulta semplice se si conosce il nome dell'istanza e se si esegue la connessione con un account membro del gruppo Administrators nel computer. Le procedure illustrate di seguito devono essere eseguite nello stesso computer che ospita [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##### <a name="to-determine-the-name-of-the-instance-of-the-database-engine"></a>Per determinare il nome dell'istanza del Motore di database  
  
1.  Accedere a Windows come membro del gruppo Administrators e aprire [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
    > [!IMPORTANT]  
    >  Se ci si connette a [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] in [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] o [!INCLUDE[nextref_longhorn](../includes/nextref-longhorn-md.md)] (o più recenti), potrebbe essere necessario fare clic con il [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] pulsante destro del mouse e quindi scegliere **Esegui come amministratore** per eseguire la connessione utilizzando le credenziali di amministratore. A partire da [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], in fase di installazione vengono aggiunti determinati account di accesso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e pertanto le credenziali di amministratore non sono necessarie.  
  
2.  Nella finestra di dialogo **Connetti al server** fare clic su **Annulla**.  
  
3.  Se Server registrati non è visualizzato, scegliere **Server registrati** dal menu **Visualizza**.  
  
4.  Dopo avere selezionato **Motore di database** nella barra degli strumenti Server registrati, espandere **Motore di database**, fare clic con il pulsante destro del mouse su **Gruppi di server locali**, scegliere **Attività**e quindi fare clic su **Registra server locali**. Verranno visualizzate tutte le istanze di [!INCLUDE[ssDE](../includes/ssde-md.md)] installate nel computer, L'istanza predefinita non è denominata e viene visualizzata come nome del computer. Un'istanza denominata viene visualizzata come nome del computer seguito da una barra rovesciata (\\) e dal nome dell'istanza. Per [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], l'istanza è denominata *<nome_computer>* \sqlexpress, se non è stato specificato un nome diverso durante l'installazione.  
  
##### <a name="to-verify-that-the-database-engine-is-running"></a>Per verificare che il Motore di database sia in esecuzione  
  
1.  In Server registrati, se accanto al nome dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è presente un punto verde con una freccia bianca, [!INCLUDE[ssDE](../includes/ssde-md.md)] è in esecuzione e non sono necessarie ulteriori operazioni.  
  
2.  Se accanto al nome dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è presente un punto rosso con un quadrato bianco, [!INCLUDE[ssDE](../includes/ssde-md.md)] non è in esecuzione. Fare clic con il pulsante destro del mouse sul nome del [!INCLUDE[ssDE](../includes/ssde-md.md)], selezionare **Controllo servizi**e quindi fare clic su **Avvia**. Dopo la visualizzazione di una finestra di conferma, dovrebbe venir avviato il [!INCLUDE[ssDE](../includes/ssde-md.md)] e il cerchio dovrebbe diventare verde con una freccia bianca.  
  
##### <a name="to-connect-to-the-database-engine"></a>Per connettersi al Motore di database  
  
1.  In [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]scegliere **Connetti Esplora oggetti** dal menu **File**.  
  
     Viene visualizzata la finestra di dialogo **Connetti al server** . Nella casella **Tipo di server** viene visualizzato l'ultimo tipo di componente usato.  
  
2.  Selezionare **Motore di database**.  
  
3.  Nella casella **Nome server** digitare il nome dell'istanza del [!INCLUDE[ssDE](../includes/ssde-md.md)]. Per l'istanza predefinita di SQL Server il nome del server è il nome del computer. Per un'istanza denominata di SQL Server, il nome del server è il *<computer_name ***\\***><* instance_name>, ad esempio **ACCTG_SRVR \SQLEXPRESS**.  
  
4.  Fare clic su **Connetti**.  
  
##  <a name="authorizing-additional-connections"></a><a name="additional"></a>Autorizzazione di connessioni aggiuntive  
 Dopo avere stabilito la connessione a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] come amministratore, una delle prime attività da svolgere consiste nell'autorizzare altri utenti a connettersi. A questo scopo è necessario creare un account di accesso e autorizzare tale account ad accedere a un database come utente. È possibile configurare account di accesso con autenticazione di Windows, che utilizzano le credenziali di Windows, o account di accesso con autenticazione di SQL Server, che archiviano le informazioni autenticate in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e sono indipendenti dalle credenziali di Windows. Se possibile, utilizzare l'autenticazione di Windows.  
  
##### <a name="create-a-windows-authentication-login"></a>Creazione di un account di accesso con autenticazione di Windows  
  
1.  Nell'attività precedente è stata eseguita la connessione a [!INCLUDE[ssDE](../includes/ssde-md.md)] utilizzando [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. In Esplora oggetti espandere l'istanza del server, espandere **Sicurezza**, fare clic con il pulsante destro del mouse su **Account di accesso**e quindi scegliere **Nuovo account di accesso**.  
  
     Viene visualizzata la finestra di dialogo **Account di accesso - Nuovo** .  
  
2.  Nella casella **nome account di accesso** della pagina **generale** Digitare un account di accesso di Windows nel formato * \<dominio>\\<account\>di accesso*.  
  
3.  Nella casella **Database predefinito** selezionare [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , se disponibile. In caso contrario, selezionare **master**.  
  
4.  Se il nuovo account di accesso sarà un account di amministrazione, selezionare **sysadmin** nella pagina **Ruoli del server**, altrimenti lasciare vuota la casella.  
  
5.  Nella pagina **Mapping utenti** selezionare **Mapping** per il database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , se disponibile. In caso contrario, selezionare **master**. Si noti che la casella **Utente** viene popolata con l'account di accesso. Alla chiusura della finestra di dialogo, nel database verrà creato questo utente.  
  
6.  Nella casella **Schema predefinito** digitare **dbo** per eseguire il mapping dell'account di accesso allo schema del proprietario del database.  
  
7.  Accettare le impostazioni predefinite delle caselle **Entità a protezione diretta** e **Stato** e fare clic su **OK** per creare l'account di accesso.  
  
> [!IMPORTANT]  
>  Si tratta delle informazioni di base necessarie per iniziare. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] offre un ambiente di sicurezza avanzato e la sicurezza rappresenta un aspetto certamente importante nell'uso dei database.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Connessione da un altro computer](lesson-2-connecting-from-another-computer.md)  
  
  
