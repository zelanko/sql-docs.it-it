---
title: Configurare Posta elettronica di SQL Server Agent per l'uso di Posta elettronica database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], SQL Server Agent Mail
- SQL Server Agent Mail
ms.assetid: 4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d3c2f5f0be09e9a60997308efd72c360348efc60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62872323"
---
# <a name="configure-sql-server-agent-mail-to-use-database-mail"></a>Configurare Posta elettronica di SQL Server Agent per l'utilizzo di Posta elettronica database
  In questo argomento viene illustrato come configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per utilizzare Posta elettronica database per inviare notifiche e avvisi in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   **Prima di iniziare:**  
  
-   [Prerequisiti](#Prerequisites)  
  
-   [Sicurezza](#Security)  
  
-   [Per configurare SQL Server Agent Mail per l'utilizzo di Posta elettronica database tramite SQL Server Management Studio](#SSMSProcedure)  
  
-   [Attività di completamento](#Follow_Up)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   Abilitare Posta elettronica database.  
  
-   Creare un account di Posta elettronica database per l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent da utilizzare.  
  
-   Creare un profilo di Posta elettronica database per l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent da utilizzare e aggiungere l'utente a **DatabaseMailUserRole** nel database **msdb** .  
  
-   Impostare il profilo come predefinito per il database **msdb** .  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per creare gli account dei profili ed eseguire le stored procedure è necessario che l'utente sia un membro del ruolo predefinito del server sysadmin.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per configurare SQL Server Agent Mail per l'utilizzo di Posta elettronica database**  
  
-   In Esplora oggetti espandere un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Fare clic con il pulsante destro del mouse su **SQL Server Agent**, quindi scegliere **Proprietà**.  
  
-   Fare clic su **Sistema avvisi**.  
  
-   Selezionare **Attiva profilo di posta**.  
  
-   Nell'elenco **Sistema di posta elettronica** selezionare **Posta elettronica database**.  
  
-   Selezionare un profilo di posta elettronica per Posta elettronica database nell'elenco **Profilo posta**.  
  
-   Riavviare SQL Server Agent.  
  
##  <a name="Follow_Up"></a> Attività di completamento  
 Le attività seguenti sono necessarie per completare la configurazione dell'agent per inviare avvisi e notifiche.  
  
-   [Avvisi](../../ssms/agent/alerts.md)  
  
     Gli avvisi possono essere configurati per segnalare a un operatore un evento di database o una condizione del sistema operativo.  
  
-   [Operatori](../../ssms/agent/operators.md)  
  
     Gli operatori solo alias di persone o gruppi che possono ricevere notifiche elettroniche  
  
  
