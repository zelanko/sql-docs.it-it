---
title: Visualizzare informazioni sui passaggi di processo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- displaying job step information
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- viewing job step information
ms.assetid: e3f06492-dc86-4e06-b186-ea58aff6d591
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3b1a4519fa83b85493cc16395e1f7c2948a84d1b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85001607"
---
# <a name="view-job-step-information"></a>Visualizzare informazioni sui passaggi di processo
  In questo argomento viene illustrato come visualizzare informazioni dettagliate sui passaggi di processo nella finestra di dialogo Proprietà passaggio processo. Sono inoltre incluse informazioni sulla visualizzazione dell'output dei passaggi di processo.  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare informazioni sui passaggi di processo mediante:**  
  
     [SQL Server Management Studio](#SSMS)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 Se un passaggio di processo è stato configurato per la scrittura dell'output in una tabella o file e il processo è stato eseguito almeno una volta, è possibile esaminare l'output nella scheda **Avanzate** della finestra di dialogo **Proprietà passaggio processo** . Quando un processo o un passaggio di processo viene eliminato, viene eliminato automaticamente anche il log di output.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È possibile visualizzare solo i processi di cui si è proprietari, a meno che non si appartenga al ruolo predefinito del server **sysadmin** . I membri di questo ruolo infatti possono visualizzare tutti i processi e tutte le informazioni sui passaggi di processo.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-job-step-information"></a>Per visualizzare informazioni sui passaggi di processo  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espandere questa istanza.  
  
2.  Espandere il nodo **SQL Server Agent**e il nodo **Processi**, fare clic con il pulsante destro del mouse sul processo che include il passaggio da visualizzare e scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà processo** fare clic sulla scheda **Passaggi** .  
  
4.  Fare clic sul passaggio di processo da visualizzare e quindi dare clic su **Modifica**.  
  
5.  Nella scheda **Generale** della finestra di dialogo **Proprietà passaggio processo** è indicato il tipo di passaggio e la funzione corrispondente.  
  
6.  Nella scheda **Avanzate** sono indicate le operazioni eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se il passaggio di processo ha esito positivo o negativo, il numero di tentativi da eseguire, la posizione in cui viene scritto l'output del passaggio e l'utente in base al quale viene eseguito il passaggio.  
  
#### <a name="to-view-job-step-output"></a>Per visualizzare l'output dei passaggi di processo  
  
1.  Nella finestra di dialogo **Proprietà passaggio processo** fare clic sulla scheda **Avanzate** .  
  
2.  A seconda della versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui si è connessi, è possibile visualizzare il file o la tabella di output dei passaggi di processo nel modo seguente:  
  
    -   Se si è connessi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o versioni successive, è possibile fare clic su **Visualizza** solo quando è selezionata l'opzione **Registra nella tabella** . In questo caso l'output dei passaggi di processo viene scritto nella tabella **sysjobstepslogs** del database **msdb** .  
  
    -   Il pulsante **Visualizza** è disabilitato quando l'output dei passaggi di processo viene scritto in un file. Per visualizzare un file di output dei passaggi di processo, utilizzare il Blocco note.  
  
  
