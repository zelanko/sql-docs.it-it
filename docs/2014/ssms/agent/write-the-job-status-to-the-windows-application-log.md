---
title: Registrare lo stato del processo nel registro applicazioni di Windows | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- SQL Server Agent jobs, status
- writing job status to log
- jobs [SQL Server Agent], status
- logs [SQL Server], jobs
ms.assetid: 3b813702-8f61-40ec-bf3b-ce9deb7e68be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 526e95490644b4fddae3e02e9ee73b57c00797c1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786723"
---
# <a name="write-the-job-status-to-the-windows-application-log"></a>Registrare lo stato del processo nel registro applicazioni di Windows
  In questo argomento viene descritto come configurare [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per registrare lo stato del processo nel log eventi dell'applicazione Windows tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o SQL Server Management Objects.  
  
 Tramite le risposte ai processi gli amministratori del database vengono informati in merito al completamento e alla frequenza di esecuzione dei processi. Le risposte ai processi tipiche includono:  
  
-   Notifica all'operatore tramite posta elettronica, trasmissione di messaggi su cercapersone o messaggi **Net Send** . Usare uno di questi metodi di risposta al processo se l'operatore dovrà eseguire operazioni basate sull'esito. Ad esempio, se un processo di backup viene completato, l'operatore dovrà ricevere una notifica per rimuovere il nastro di backup e riporlo in un luogo sicuro.  
  
-   Scrittura di un messaggio di evento nel registro delle applicazioni di Windows. Questa risposta può essere usata esclusivamente per i processi non riusciti.  
  
-   Eliminazione automatica del processo. Usare la risposta soltanto se si è certi che non sarà necessario rieseguire il processo.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per scrivere lo stato del processo nel registro applicazioni di Windows usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-write-job-status-to-the-windows-application-log"></a>Per registrare lo stato del processo nel registro applicazioni di Windows  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**, espandere **Processi**, fare clic con il pulsante destro del mouse sul processo da modificare e quindi scegliere **Proprietà**.  
  
3.  Scegliere la pagina **Notifiche** .  
  
4.  Selezionare l'opzione **Scrivi nel registro eventi delle applicazioni di Windows**e quindi scegliere una delle opzioni seguenti:  
  
    -   Fare clic su**In caso di esito positivo processo**per registrare lo stato del processo quando questo viene completato correttamente.  
  
    -   Fare clic su**In caso di esito negativo processo**per registrare lo stato del processo quando questo non viene completato correttamente.  
  
    -   Fare clic su**Al termine del processo** per registrare lo stato del processo indipendentemente dal suo completamento.  
  
##  <a name="SMO"></a> Utilizzo di SQL Server Management Objects  
 **Per registrare lo stato del processo nel registro applicazioni di Windows**  
  
 Chiamare la proprietà `EventLogLevel` della classe `Job` tramite un linguaggio di programmazione come Visual Basic, Visual C# o PowerShell.  
  
 Nell'esempio di codice seguente il processo viene impostato per generare una voce nel registro eventi del sistema operativo al termine dell'esecuzione del processo.  
  
 **PowerShell**  
  
```  
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = new-object Microsoft.SqlServer.Management.Smo.Agent.Job($srv.JobServer, "Test Job")  
$jb.EventLogLevel = [Microsoft.SqlServer.Management.Smo.Agent.CompletionAction]::Always  
```  
  
  
