---
title: Proprietà server di pubblicazione di replica di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distpubproperties.f1
- sql12.rep.configdistwizard.pubproperties.general.f1
- sql12.rep.configdistwizard.pubproperties.pubdb.f1
- sql12.rep.configdistwizard.pubproperties.subscribers.f1
ms.assetid: 98df1aea-0406-40bf-a917-4bd80464125c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2ea467b00223e31ec7672d4d54a49150cf05368c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63261980"
---
# <a name="sql-server-replication-publisher-properties"></a>Proprietà server di pubblicazione di replica di SQL Server
  In questa sezione contiene informazioni sulle proprietà di server di pubblicazione disponibili nel server di distribuzione e il server di pubblicazione. 

## <a name="general"></a>Generale  
  La pagina **Generale** della finestra di dialogo **Proprietà server di pubblicazione** visualizza informazioni di sola lettura sul server di distribuzione e sul database di distribuzione utilizzati dal server di pubblicazione. Per modificare il server di distribuzione o il database di distribuzione per un server di pubblicazione, eseguire le operazioni seguenti:  
  
1.  Disabilitare la pubblicazione nel server di pubblicazione. Per altre informazioni, vedere [Disabilitare la pubblicazione e la distribuzione](disable-publishing-and-distribution.md).    
2.  Riconfigurare la pubblicazione e la distribuzione. Per altre informazioni, vedere [Configure Publishing and Distribution](configure-publishing-and-distribution.md).  

## <a name="distributor"></a>Database di distribuzione
  La finestra di dialogo **Proprietà server di pubblicazione** consente di visualizzare e modificare le proprietà associate alla relazione tra il server di pubblicazione e il relativo server di distribuzione.  
  
### <a name="options"></a>Opzioni  
 **Connessione agente al server di pubblicazione**  
 Consente di specificare il contesto in cui gli agenti indicati di seguito creeranno connessioni dal server di distribuzione al server di pubblicazione:  
  
-   Agente di lettura coda per pubblicazioni transazionali che consentono sottoscrizioni ad aggiornamento in coda.  
  
-   Agente snapshot e agente di lettura log per pubblicazioni Oracle.  
  
 Selezionare **Rappresenta l'account del processo dell'agente** per stabilire una connessione al server di pubblicazione tramite il contesto dell'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con cui vengono eseguiti gli agenti oppure specificare **Autenticazione di SQL Server**e quindi immettere un valore per **Nome account di accesso** e **Password**. È consigliabile scegliere l'opzione **Rappresenta l'account del processo dell'agente**. Per altre informazioni sulla sicurezza dell'agente, vedere [Modello di sicurezza dell'agente di replica](security/replication-agent-security-model.md).  
  
 Gli account di Windows con cui vengono eseguiti questi agenti sono specificati nella Creazione guidata nuova pubblicazione. È possibile modificare gli account seguenti:  
  
-   Nella finestra di dialogo **Proprietà server di distribuzione** per l'agente di lettura coda.  
  
-   Nella finestra di dialogo **Proprietà server di pubblicazione** per gli agenti snapshot e di lettura log.  
  
 **Varie**  
 Le proprietà **Tipo server di pubblicazione** e **Nome database di distribuzione** sono di sola lettura. La proprietà **Cartella snapshot predefinita** può essere modificata. Per altre informazioni sulla cartella snapshot, vedere [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md).  
  

## <a name="publication-databases"></a>Database di pubblicazione
  La pagina **Database di pubblicazione** della finestra di dialogo **Proprietà server di pubblicazione** consente a un utente membro del ruolo predefinito del server **sysadmin** di abilitare i database per la replica. L'abilitazione di un database non ne implica la sua pubblicazione, ma consente a qualsiasi utente membro del ruolo predefinito del database **db_owner** per tale database di creare una o più pubblicazioni sul database.  
  
### <a name="options"></a>Opzioni  
 **Transazionale**  
 Selezionare questa casella di controllo per consentire agli utenti membri del ruolo predefinito del database **db_owner** di creare pubblicazioni snapshot o pubblicazioni transazionali nel database. 
  
 **Merge**  
 Selezionare questa casella di controllo per consentire agli utenti membri del ruolo predefinito del database **db_owner** di creare pubblicazioni di tipo merge nel database.  

## <a name="subscribers"></a>Sottoscrittori

  La pagina **Sottoscrittori** della finestra di dialogo **Proprietà server di pubblicazione** viene utilizzata per i server di pubblicazione che eseguono versioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Questa pagina consente di abilitare i Sottoscrittori al ricevimento di dati dalle pubblicazioni incluse nel server di pubblicazione corrente. L'abilitazione di un Sottoscrittore al ricevimento di dati dal server di pubblicazione corrente non crea sottoscrizioni delle pubblicazioni incluse nel server di pubblicazione. Per creare una sottoscrizione è necessario utilizzare la Creazione guidata nuova sottoscrizione.  
  
### <a name="options"></a>Opzioni  
 **Sottoscrittori**  
 La griglia delle proprietà **Sottoscrittori** visualizza i Sottoscrittori abilitati al ricevimento di dati dalle pubblicazioni incluse nel server di pubblicazione corrente. Per visualizzare e impostare proprietà aggiuntive fare clic sul pulsante delle proprietà (**...**) accanto a un Sottoscrittore.  
  
 **Aggiungi**  
 Fare clic su **Aggiungi** per aggiungere un Sottoscrittore e quindi fare clic su **Aggiungi Sottoscrittore SQL Server** o su **Aggiungi Sottoscrittore non SQL Server**.  

## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md)   

  
  
