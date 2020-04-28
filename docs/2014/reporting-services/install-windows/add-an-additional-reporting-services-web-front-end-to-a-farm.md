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
ms.openlocfilehash: 6dba2c6637c9a637e60583b926b9e80671c043be
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78173520"
---
# <a name="add-an-additional-reporting-services-web-front-end-to-a-farm"></a>Aggiungere un ulteriore front-end Web di Reporting Services a una farm
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] La modalità SharePoint include i componenti necessari per server applicazioni e server front-end Web (WFE). Questo argomento è incentrato sull'installazione dei componenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] obbligatori per un server WFE, incluse le pagine di applicazione utilizzate dalle funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , ad esempio sottoscrizioni, avvisi dati e [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. L'installazione primaria di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] necessaria per un server WFE consiste nell'installare il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per i prodotti SharePoint 2010.

## <a name="prerequisites"></a>Prerequisites

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

 ![Aggiungere SSRS e un nuovo front-end Web di SharePoint](../../../2014/sql-server/install/media/rs-sharepointscale-wfe.gif "Aggiungere SSRS e un nuovo front-end Web di SharePoint")

 Nei seguenti passaggi si presuppone che l'installazione e la configurazione del server vengano eseguite da un amministratore.

|Passaggio|Descrizione e collegamento|
|----------|--------------------------|
|Eseguire l'Utilità preparazione prodotti SharePoint 2010.|È necessario disporre dei supporti di installazione di SharePoint 2010. L'utilità di preparazione corrisponde al file **PrerequisiteInstaller.exe** disponibile nei supporti di installazione.|
|Installare un prodotto SharePoint 2010.|1) selezionare il tipo di installazione **server farm** .<br /><br /> 2) selezionare **completa** per il tipo di server.<br /><br /> 3) Una volta completata l'installazione, non eseguire la Configurazione guidata Prodotti SharePoint se nella farm di SharePoint esistente è installato SharePoint 2010 SP1. È necessario installare SharePoint SP1 prima di eseguire la Configurazione guidata Prodotti SharePoint.|
|Installare SharePoint Server 2010 SP1.|Se nella farm di SharePoint esistente è installato SharePoint 2010 SP1, scaricare e installare SharePoint 2010 SP1[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697)da:.<br /><br /> Per ulteriori informazioni su SharePoint 2010 SP1, vedere [Problemi noti durante l'installazione di Office 2010 SP1 e SharePoint 2010 SP1](https://support.microsoft.com/kb/2532126):|
|Eseguire la Configurazione guidata Prodotti SharePoint per aggiungere il server alla farm.|1) nel gruppo di programmi **prodotti Microsoft sharepoint 2010** fare clic su **Configurazione guidata prodotti Microsoft SharePoint 2010**.<br /><br /> 2) nella pagina **connessione a una server farm** selezionare **Connetti a una farm esistente** e fare clic su **Avanti**.<br /><br /> 3) nella pagina **specifica impostazioni database di configurazione** Digitare il nome del server di database utilizzato per la farm esistente e il nome del database di configurazione. Fare clic su **Avanti**.<br />**&#42;&#42; importanti &#42;&#42;** Se viene visualizzato un messaggio di errore simile al seguente ed è stata verificata l'autorizzazione, verificare che i protocolli siano abilitati per la configurazione di rete SQL Server in **SQL Server Configuration Manager**. "Impossibile connettersi al server di database. Verificare che il database esista, che sia un server SQL e di disporre delle autorizzazioni appropriate per accedere al server. "<br />**&#42;&#42; importanti &#42;&#42;** Se viene visualizzata la pagina relativa **allo stato della patch e del prodotto della server farm**, sarà necessario esaminare le informazioni nella pagina e aggiornare il server con i file necessari prima di poter procedere con l'aggiunta del server alla farm.<br /><br /> 4) nella pagina **specifica impostazioni sicurezza farm** Digitare la passphrase della farm e fare clic su **Avanti**. Scegliere **Avanti** nella pagina di configurazione per eseguire la procedura guidata.<br /><br /> 5) fare clic su **Avanti** per eseguire la **Configurazione guidata della farm**.|
|Verificare che il server sia stato aggiunto alla farm di SharePoint.|1) Nel gruppo **Impostazioni di sistema** di Amministrazione centrale SharePoint fare clic su **Gestisci server della farm** .<br /><br /> 2) Verificare che il nuovo server sia stato aggiunto e che lo stato sia corretto.<br /><br /> 3) per rimuovere questo server dal ruolo WFE, fare clic su **Gestisci servizi nel server** e arrestare il servizio **applicazione Web Microsoft SharePoint Foundation**.|
|Installare il [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] componente aggiuntivo per prodotti SharePoint 2010.|Esistono diversi metodi per l'installazione del componente aggiuntivo. Nei seguenti passaggi viene utilizzata l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Per ulteriori informazioni sull'installazione del componente aggiuntivo, vedere [installare o disinstallare il componente aggiuntivo Reporting Services per sharepoint &#40;sharepoint 2010 e sharepoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). Eseguire [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] l'installazione:<br /><br /> 1) Nella pagina **Impostazione ruolo** selezionare **Installazione funzionalità SQL Server**<br /><br /> 2) nella pagina **Selezione funzionalità** selezionare **Reporting Services componente aggiuntivo per prodotti SharePoint** .<br /><br /> 3) fare clic su **Avanti** nelle diverse pagine successive per completare le opzioni di installazione.<br /><br /> Per ulteriori informazioni sull'installazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]di, vedere [Install Reporting Services modalità sharepoint per SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|
|Verificare che il nuovo server di report sia operativo.|1) Nel gruppo **Impostazioni di sistema** di Amministrazione centrale SharePoint fare clic su **Gestisci server della farm** .<br /><br /> 2) Verificare che il nuovo server sia presente nell'elenco.|
|Aggiornare la soluzione NLB.|Se necessario, aggiornare l'ambiente NLB hardware o software per includere il nuovo server.|

## <a name="see-also"></a>Vedere anche
 [Aggiungere un server Web o un server applicazioni alla farm (SharePoint server 2010) configurare i](https://technet.microsoft.com/library/bb218968.aspx?missingurl=%2fen-us%2flibrary%2fe1aeaddf-6ee4-43a9-82b7-db20b68c71db\(Office.14\)) [Servizi (SharePoint Server 2010)](https://technet.microsoft.com/library/ee794878.aspx)


