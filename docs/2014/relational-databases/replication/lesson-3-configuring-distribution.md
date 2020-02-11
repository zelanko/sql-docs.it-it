---
title: 'Lezione 3: Configurazione della distribuzione | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 8d873d3664c88963b17550734b488e6872a9cc84
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721103"
---
# <a name="lesson-3-configuring-distribution"></a>Lezione 3: Configurazione della distribuzione
  In questa lezione verrà configurata la distribuzione nel server di pubblicazione e verranno impostate le autorizzazioni necessarie per i database di pubblicazione e di distribuzione. Se il server di distribuzione è già stato configurato, è necessario disabilitare la pubblicazione e la distribuzione prima di iniziare questa lezione. Non eseguire questa operazione se è necessario mantenere la topologia di replica esistente.  
  
 In questa esercitazione non è prevista la configurazione del server di pubblicazione con un server di distribuzione remoto.  
  
### <a name="configuring-distribution-at-the-publisher"></a>Configurazione della distribuzione nel server di pubblicazione  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **Replica** e scegliere **Configura distribuzione**.  
  
    > [!NOTE]  
    >  Se è stata effettuata la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando **localhost** anziché il nome effettivo del server, verrà visualizzato un avviso in cui viene indicata l'impossibilità di stabilire una connessione tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il server **'localhost'**. Fare clic su **OK** nella finestra di dialogo di avviso. Nella finestra di dialogo **Connetti al server** modificare **Nome server** sostituendo **localhost** con il nome del server. Fare clic su **Connetti**.  
  
     Verrà avviata la Configurazione guidata distribuzione.  
  
3.  Nella pagina **server di distribuzione** selezionare **'**_\<nomeserver>_' fungerà **da server di distribuzione per se stesso. SQL Server creerà un database di distribuzione e un log**e quindi fare clic su **Avanti**.  
  
4.  Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in esecuzione, nella pagina [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agent** selezionare **Sì**e configurare l'avvio automatico del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Fare clic su **Avanti**.  
  
5.  Immettere ** \\ ** \< _Machine_Name>_ **\repldata** nella casella di testo **cartella snapshot** , in \<cui *Machine_Name>* è il nome del server di pubblicazione, quindi fare clic su **Avanti**.  
  
6.  Accettare i valori predefiniti nella pagine seguenti della procedura guidata.  
  
7.  Fare clic su **Fine** per abilitare la distribuzione.  
  
### <a name="setting-database-permissions-at-the-publisher"></a>Impostazione delle autorizzazioni per il database nel server di pubblicazione  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere **sicurezza**, fare clic con il pulsante destro del mouse su **account di accesso**, quindi scegliere **nuovo account di accesso**.  
  
2.  Nella pagina **generale** fare clic su **Cerca**, immettere \< _Machine_Name>_ **\ repl_snapshot** nella casella **immettere il nome dell'oggetto da selezionare** , dove \< *Machine_Name>* è il nome del server di pubblicazione locale, fare clic su **Controlla nomi**e quindi su **OK**.  
  
3.  Nell'elenco utenti con mapping **a questo account di accesso** nella pagina **mapping** utenti selezionare i database **** e [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] la distribuzione.  
  
     Nell'elenco **appartenenza a ruoli del database** selezionare `db_owner` il ruolo per l'account di accesso per entrambi i database.  
  
4.  Fare clic su **OK** per creare l'account di accesso.  
  
5.  Ripetere i passaggi da 1 a 4 per creare un account di accesso per l'account locale repl_logreader. È necessario eseguire il mapping di questo account di accesso anche agli utenti `db_owner` che sono membri del ruolo predefinito del database nei database **AdventureWorks** e di **distribuzione** .  
  
6.  Ripetere i passaggi da 1 a 4 per creare un account di accesso per l'account locale repl_distribution. È necessario eseguire il mapping di questo account di accesso a un utente membro `db_owner` del ruolo predefinito del database nel database di **distribuzione** .  
  
7.  Ripetere i passaggi da 1 a 4 per creare un account di accesso per l'account locale repl_merge. Questo account deve avere mapping di utenti nel database di **distribuzione** e nel database **AdventureWorks** .  
  
## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](configure-distribution.md)   
 [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md)  
  
  
