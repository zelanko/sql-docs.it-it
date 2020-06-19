---
title: Designare un server di inoltri eventi (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1617038a42dcef9103613e4d0164ba0f796000fa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995278"
---
# <a name="designate-an-events-forwarding-server-sql-server-management-studio"></a>Designate an Events Forwarding Server (SQL Server Management Studio)
  In questo argomento viene descritto come designare un server al quale vengono [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trasmessi gli eventi in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Si noti che l'inoltro di eventi si applica agli eventi inoltrati tra server, non agli eventi inoltrati tra istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ospitate in un singolo computer. Notare inoltre che per ricevere eventi inoltrati, il server di gestione degli avvisi deve essere un'istanza predefinita di SQL Server.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per impostare un server di inoltro eventi utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>Per impostare un server di inoltro eventi  
  
1.  In **Esplora oggetti** fare clic sul segno più per espandere il server da cui si desidera inoltrare gli eventi a un altro server.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent** e scegliere **Proprietà**.  

3.  Nella finestra di dialogo **Proprietà SQL Server Agent -**_nome_server_ fare clic su **Avanzate** in **Selezione pagina**.  

4.  In **Inoltro eventi SQL Server**selezionare la casella di controllo **Inoltra eventi a un altro server** .  
  
5.  Nell'elenco **Server** fare clic su un server e quindi in **Eventi**selezionare una delle opzioni seguenti:  
  
    -   Selezionare **Eventi non gestiti** per inoltrare solo gli eventi che non sono stati gestiti da avvisi locali.  
  
    -   Selezionare **Tutti gli eventi** per inoltrare tutti gli eventi, indipendentemente dal fatto che siano stati gestiti o meno da avvisi locali.  
  
6.  Nell'elenco **Eventi con gravità maggiore o uguale a** selezionare il livello di gravità che contraddistingue gli eventi da inoltrare al server selezionato.  
  
7.  Al termine, fare clic su **OK**.  
  
  
