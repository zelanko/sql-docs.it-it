---
title: Impostare l'arresto dell'esecuzione del processo (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca9343fe8a6f9e89ba9f26dbbbb12dd7362aff91
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63033603"
---
# <a name="set-job-execution-shutdown-sql-server-management-studio"></a>Set Job Execution Shutdown (SQL Server Management Studio)
  In questo argomento viene descritto come impostare il periodo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di attesa di Agent prima che l'esecuzione dei processi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] venga completata prima che [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] l'agente [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]venga terminato in tramite.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per impostare un'ora di arresto per un processo di SQL Server Agent utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per impostazione predefinita, i membri del ruolo predefinito del server **sysadmin** possono impostare il periodo di attesa di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent prima di terminare l'esecuzione dei processi, trascorso il quale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent stesso viene interrotto. Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>Per impostare l'arresto dell'esecuzione del processo  
  
1.  In **Esplora oggetti** fare clic sul segno più per espandere il server in cui si desidera impostare un intervallo per l'arresto dell'esecuzione del processo.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent** e scegliere **Proprietà**.  
  
3.  In **Selezione pagina**selezionare **Sistema processi**.  
  
4.  Impostare l'opzione **Intervallo di time-out chiusura** (in secondi) per aumentare o ridurre l'intervallo di time-out di chiusura. Questo valore determina l'intervallo di attesa del completamento dell'esecuzione dei processi da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, trascorso il quale viene interrotto anche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
  
