---
title: Opzioni (pagina risultati query e servizi di dipendenza) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.DependencyServicesGeneral
ms.assetid: dd7f6c31-7d7f-4972-854a-1419a2826dca
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d19228fdf17788e9118367a6f0f0eb3be90cb72a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930132"
---
# <a name="options-query-results-and-dependency-services-page"></a>Opzioni (Risultati delle query e pagina Servizi di dipendenza)
  Utilizzare questa pagina per specificare il server a cui connettersi per utilizzare Servizi di dipendenza. Servizi di dipendenza consente di estrarre informazioni sulle dipendenze tra oggetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] archiviati in server diversi. Per visualizzare le dipendenze degli oggetti, utilizzare la finestra di dialogo **Dipendenze oggetti** in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] .  
  
 **Per saperne di più**  
  
1.  [Aprire la finestra di dialogo Opzioni (pagina Risultati query/Servizi di dipendenza)](#open_dialog)  
  
2.  [Configurare le opzioni](#options)  
  
##  <a name="open-the-options-query-resultsdependency-services-page-dialog-box"></a><a name="open_dialog"></a>Aprire la finestra di dialogo Opzioni (pagina risultati query/servizi di dipendenza)  
  
1.  In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] fare clic su **Opzioni** nel menu **strumenti** .  
  
2.  Espandere **Risultati query** e fare clic su **Servizi di dipendenza**.  
  
##  <a name="configure-the-options"></a><a name="options"></a>Configurare le opzioni  
  
### <a name="options"></a>Opzioni  
 **Server Servizi di dipendenza**  
 Consente di specificare il server in cui è installato Servizi di dipendenza.  
  
 **autenticazione**  
 Selezionare l'autenticazione di Windows per accedere utilizzando un account utente di Microsoft Windows oppure selezionare l'autenticazione di SQL Server.  
  
 Quando un utente si connette con un nome di account di accesso e una password da una connessione non trusted, SQL Server esegue l'autenticazione controllando se è stato impostato un account di accesso di SQL Server e se la password specificata corrisponde a quella registrata in precedenza. Se SQL Server non è in grado di trovare un account di accesso, l'autenticazione non riesce e viene visualizzato un messaggio di errore.  
  
 **Nome utente**  
 Se si utilizza l'autenticazione di SQL Server, specificare un nome utente.  
  
 **Password**  
 Se si utilizza l'autenticazione di SQL Server, specificare una password.  
  
 **Test**  
 Fare clic su questa opzione per testare la connessione.