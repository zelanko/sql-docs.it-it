---
title: Eliminare automaticamente un processo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- dropping jobs
- SQL Server Agent jobs, removing
- automatic job removal
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 92dbb6da-5919-4bde-9354-d454e9ea3da0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42538ac6566b70105fd183da1cadd00f7fd0c13b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011788"
---
# <a name="automatically-delete-a-job"></a>Automatically Delete a Job
  In questo argomento viene descritto come configurare [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per eliminare automaticamente i processi in caso di esito positivo, esito negativo o completamento tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o SQL Server Management Objects.  
  
 Tramite le risposte ai processi gli amministratori del database vengono informati in merito al completamento e alla frequenza di esecuzione dei processi. Le risposte ai processi tipiche includono:  
  
-   Notifica all'operatore tramite posta elettronica, trasmissione di messaggi su cercapersone o messaggi **Net Send** .  
  
     Usare uno di questi metodi di risposta al processo se l'operatore dovrà eseguire operazioni basate sull'esito. Ad esempio, se un processo di backup viene completato, l'operatore dovrà ricevere una notifica per rimuovere il nastro di backup e riporlo in un luogo sicuro.  
  
-   Scrittura di un messaggio di evento nel registro delle applicazioni di Windows.  
  
     Questa risposta può essere usata esclusivamente per i processi non riusciti.  
  
-   Eliminazione automatica del processo.  
  
     Usare la risposta soltanto se si è certi che non sarà necessario rieseguire il processo.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per specificare le risposte ai processi utilizzando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-automatically-delete-a-job"></a>Per eliminare automaticamente un processo  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espandere questa istanza.  
  
2.  Espandere **SQL Server Agent**, espandere **Processi**, fare clic con il pulsante destro del mouse sul processo da modificare e quindi scegliere **Proprietà**.  
  
3.  Scegliere la pagina **Notifiche** .  
  
4.  Selezionare **Elimina il processo automaticamente**e quindi eseguire una delle operazioni seguenti:  
  
    -   Selezionare **In caso di esito positivo processo** per eliminare lo stato del processo quando questo viene completato con esito positivo.  
  
    -   Selezionare **In caso di esito negativo processo** per eliminare il processo quando questo viene completato con esito negativo.  
  
    -   Selezionare **Al termine del processo** per eliminare il processo indipendentemente dall'esito con cui viene completato.  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Utilizzo di SQL Server Management Objects  
 **Per eliminare automaticamente un processo**  
  
 Utilizzare la proprietà `DeleteLevel` della classe `Job` tramite un linguaggio di programmazione come Visual Basic, Visual C# o PowerShell. Per altre informazioni, vedere [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
