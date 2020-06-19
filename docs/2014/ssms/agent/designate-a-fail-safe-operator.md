---
title: Impostare un operatore alternativo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- fail-safe operator [SQL Server]
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 0f4eb513-5c0a-4523-974e-e85c1deeb57f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 73eb11034d185deb9c004d138230fff8fbf27bb6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995288"
---
# <a name="designate-a-fail-safe-operator"></a>Impostazione di un operatore alternativo
  Un operatore alternativo è un utente che riceve l'avviso nel caso in cui l'operatore designato non sia raggiungibile. In questo argomento viene descritto come impostare un operatore alternativo per la ricezione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] notifiche di avviso di Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per impostare un operatore alternativo utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Le opzioni Cercapersone e **net send** verranno rimosse da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in una versione futura di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Evitare pertanto di utilizzarle in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui sono state implementate.  
  
-   Si noti che per inviare notifiche tramite posta elettronica e cercapersone agli operatori, è necessario configurare SQL Server Agent per l'utilizzo di Posta elettronica database. Per ulteriori informazioni, vedere [Procedura: Assegnazione di avvisi a un operatore (SQL Server Management Studio)](assign-alerts-to-an-operator.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è incluso un semplice strumento grafico per la gestione dei processi, che è lo strumento consigliato per la creazione e la gestione dell'infrastruttura dei processi.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono definire operatori alternativi.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-designate-a-fail-safe-operator"></a>Per impostare un operatore alternativo  
  
1.  In **Esplora oggetti** fare clic sul segno più per espandere il server che contiene l'operatore di SQL Server Agent che si vuole definire come alternativo.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent** e scegliere **Proprietà**.  

3.  Nella finestra di dialogo **proprietà SQL Server Agent-**_server_name_ , in **Selezione pagina**selezionare **sistema avvisi**.  
 
4.  In **Operatore alternativo**selezionare **Abilita operatore alternativo**.  
  
5.  Nell'elenco **Operatore** selezionare l'operatore che si vuole rendere alternativo.  
  
6.  Selezionare tutte le caselle di controllo necessarie a specificare come l'operatore riceverà la notifica: **Posta elettronica**, **Cercapersone**o **Net Send**.  
  
7.  Al termine, fare clic su **OK**.  
  
  
