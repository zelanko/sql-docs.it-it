---
title: Aggiungere un ulteriore front-end Web di Reporting Services a una farm | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d7a11bda-ae26-49ac-b071-37d83cae5afe
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a7996ea2541963d0c7a2060d819667e25d102305
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108956"
---
# <a name="add-an-additional-reporting-services-web-front-end-to-a-farm"></a>Aggiungere un ulteriore front-end Web di Reporting Services a una farm
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] La modalità SharePoint include i componenti necessari per server applicazioni e server front-end Web (WFE). Questo argomento è incentrato sull'installazione dei componenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] obbligatori per un server WFE, incluse le pagine di applicazione utilizzate dalle funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , ad esempio sottoscrizioni, avvisi dati e [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. L'installazione primaria di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] necessaria per un server WFE consiste nell'installare il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per i prodotti SharePoint 2010.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   Per eseguire il programma di installazione di SQL Server, è necessario essere un amministratore locale.  
  
-   Il computer deve fare parte di un dominio.  
  
-   È inoltre necessario conoscere il nome del server di database esistente che ospita i database di configurazione e del contenuto di SharePoint.  
  
-   Il server di database deve essere configurato in modo da consentire le connessioni ai database remoti.  In caso contrario, non sarà possibile creare un join del nuovo server alla farm, in quanto il nuovo server non sarà in grado di stabilire una connessione ai database di configurazione di SharePoint.  
  
-   Nel nuovo server dovrà essere installata la stessa versione di SharePoint in esecuzione sui server della farm correnti. Se nella farm è già installato, ad esempio, SharePoint 2010 Service Pack 1 (SP1), sarà necessario installare SP1 anche nel nuovo server prima di poterne creare un join alla farm.  
  
-   Esaminare gli argomenti aggiuntivi seguenti per comprendere i requisiti relativi al sistema e alla versione:  
  
     [Guida per l'utilizzo delle funzionalità di Business Intelligence di SQL Server in una farm di SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>Passaggi  
 Nei passaggi di questo argomento si presuppone che l'installazione e la configurazione del server vengano eseguite da un amministratore della farm di SharePoint. Nel diagramma è illustrato un tipico ambiente a tre livelli e gli elementi numerati nel diagramma sono descritti nell'elenco seguente:  
  
-   (1) Più server front-end Web (WFE). I server front-end Web richiedono il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per SharePoint 2010. Nei passaggi seguenti viene aggiunto un secondo server applicazioni a questo livello.  
  
-   (2) Due server applicazioni che eseguono [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e siti Web, ad esempio Amministrazione centrale.  
  
-   (3) Due server di database SQL Server.  
  
-   (4) Rappresenta una soluzione software o hardware di bilanciamento del carico di rete.  
  
 ![Aggiungere SSRS a un nuovo WFE di SharePoint](../../../2014/sql-server/install/media/rs-sharepointscale-wfe.gif "Aggiungere SSRS a un nuovo WFE di SharePoint")  
  
 Nei seguenti passaggi si presuppone che l'installazione e la configurazione del server vengano eseguite da un amministratore.  
  
|Passaggio|Descrizione e collegamento|  
|----------|--------------------------|  
|Eseguire l'Utilità preparazione prodotti SharePoint 2010.|È necessario disporre dei supporti di installazione di SharePoint 2010. L'utilità di preparazione corrisponde al file **PrerequisiteInstaller.exe** disponibile nei supporti di installazione.|  
|Installare un prodotto SharePoint 2010.|1) selezionare il **Server Farm** tipo di installazione.<br /><br /> 2) selezionare **completa** per il tipo di server.<br /><br /> 3) Una volta completata l'installazione, non eseguire la Configurazione guidata Prodotti SharePoint se nella farm di SharePoint esistente è installato SharePoint 2010 SP1. È necessario installare SharePoint SP1 prima di eseguire la Configurazione guidata Prodotti SharePoint.|  
|Installare SharePoint Server 2010 SP1.|Se nella farm di SharePoint esistente è installato SharePoint 2010 SP1 scaricare e installare SharePoint 2010 SP1 da:[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697).<br /><br /> Per ulteriori informazioni su SharePoint 2010 SP1, vedere [Problemi noti durante l'installazione di Office 2010 SP1 e SharePoint 2010 SP1](https://support.microsoft.com/kb/2532126):|  
|Eseguire la Configurazione guidata Prodotti SharePoint per aggiungere il server alla farm.|1) nella **prodotti Microsoft SharePoint 2010** gruppo di programmi, fare clic su **configurazione guidata prodotti di Microsoft SharePoint 2010**.<br /><br /> 2) nella **Connetti a una Server Farm** pagina Scegli **Connetti a una Farm esistente** e fare clic su **Next**.<br /><br /> 3) nella **specifica impostazioni Database di configurazione** , digitare il nome del server di database utilizzato per la farm esistente e il nome del database di configurazione. Scegliere **Avanti**.<br />**&#42;&#42;Importante &#42; &#42;**  se viene visualizzato un messaggio di errore simile al seguente ed è stata verificata la disponibilità delle autorizzazioni, quindi verificare che i protocolli sono abilitati per la configurazione di rete SQL Server nelle **Sql Server Configuration Manager**. "Impossibile connettersi al server di database. Verificare che il database esista, sia un Sql Server e di disporre delle autorizzazioni appropriate per accedere al server."<br />**&#42;&#42;Importante &#42; &#42;**  se viene visualizzata la pagina **stato di Patch e prodotti nella Server Farm**, sarà necessario esaminare le informazioni nella pagina e aggiornare il server con i file necessari prima di procedere con l'aggiunta il server alla farm.<br /><br /> 4) nella **specifica impostazioni sicurezza Farm** digitare la passphrase della farm e fare clic su **successivo**. Scegliere **Avanti** nella pagina di configurazione per eseguire la procedura guidata.<br /><br /> 5) fare clic su **successivo** per eseguire il **configurazione guidata Farm**.|  
|Verificare che il server sia stato aggiunto alla farm di SharePoint.|1) Nel gruppo **Impostazioni di sistema** di Amministrazione centrale SharePoint fare clic su **Gestisci server della farm** .<br /><br /> 2) Verificare che il nuovo server sia stato aggiunto e che lo stato sia corretto.<br /><br /> 3) per rimuovere questo server dal ruolo WFE, fare clic su **Gestisci servizi nel server** e arrestare il servizio **applicazione Web di Microsoft SharePoint Foundation**.|  
|Installare il [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aggiuntivo per prodotti SharePoint 2010.|Esistono diversi metodi per l'installazione del componente aggiuntivo. Nei seguenti passaggi viene utilizzata l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Per altre informazioni sull'installazione il componente aggiuntivo, vedere [installare o disinstallare il componente aggiuntivo di Reporting Services per SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). Eseguire [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] installazione:<br /><br /> 1) Nella pagina **Impostazione ruolo** selezionare **Installazione funzionalità SQL Server**<br /><br /> 2) nella **selezione delle caratteristiche** pagina, selezionare **componente aggiuntivo di Reporting Services per prodotti SharePoint**<br /><br /> 3) fare clic su **successivo** in diverse pagine successive per completare le opzioni di installazione.<br /><br /> Per altre informazioni sull'installazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [installare Reporting Services SharePoint Mode for SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Verificare che il nuovo server di report sia operativo.|1) Nel gruppo **Impostazioni di sistema** di Amministrazione centrale SharePoint fare clic su **Gestisci server della farm** .<br /><br /> 2) Verificare che il nuovo server sia presente nell'elenco.|  
|Aggiornare la soluzione NLB.|Se necessario, aggiornare l'ambiente NLB hardware o software per includere il nuovo server.|  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere un sito Web o un server applicazioni alla farm (SharePoint Server 2010)](https://technet.microsoft.com/library/bb218968.aspx?missingurl=%2fen-us%2flibrary%2fe1aeaddf-6ee4-43a9-82b7-db20b68c71db\(Office.14\))   
 [Configurare i servizi (SharePoint Server 2010)](https://technet.microsoft.com/library/ee794878.aspx)  
  
  
