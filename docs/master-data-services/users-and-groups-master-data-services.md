---
title: Utenti e gruppi (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- users [Master Data Services]
- groups [Master Data Services]
- users [Master Data Services], about users
- groups [Master Data Services], about groups
ms.assetid: ed08dd2d-248e-4b68-91d4-e9961cb50eed
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bba9009365a4353a6fc5610fe97b6c859ea8910f
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484950"
---
# <a name="users-and-groups-master-data-services"></a>Utenti e gruppi (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Per accedere all'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] l'utente deve disporre di un account di dominio di Windows o di un account nel computer server in cui è installato [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Per concedere l'accesso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] è possibile:  
  
-   Aggiungere l'account utente a un dominio o a un gruppo locale e aggiungere il gruppo all'elenco di gruppi in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
-   Aggiungere l'account utente all'elenco di utenti in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
    > [!NOTE]  
    >  Quando un utente appartiene a un gruppo che dispone dell'accesso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], il nome dell'utente viene aggiunto automaticamente all'elenco di utenti al primo accesso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] o a MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
 Per eseguire azioni nell'area funzionale **Visualizzatore** dell'interfaccia utente, è necessario assegnare al gruppo o all'utente l'autorizzazione di accesso all'area funzionale **Visualizzatore** e l'autorizzazione per gli oggetti modello.  
  
 Se un utente o un gruppo deve accedere ad altre aree funzionali, sarà necessario assegnare all'utente o al gruppo l'accesso all'area funzionale specifica.  
  
## <a name="best-practice"></a>Procedura consigliata  
 Per semplificare l'amministrazione, creare gruppi e assegnare a ognuno di essi l'autorizzazione per aree funzionali e oggetti modello. È quindi possibile aggiungere e rimuovere utenti dai gruppi senza accedere all'interfaccia utente di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
 Non assegnare autorizzazioni aggiuntive a un singolo utente e non includere un utente in più gruppi che dispongono dell'accesso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Non utilizzare autorizzazioni membri gerarchia, a meno che non si desideri che un gruppo disponga di accesso limitato a membri specifici.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere un utente &#40;Master Data Services&#41;](../master-data-services/add-a-user-master-data-services.md)   
 [Aggiungere un gruppo &#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)   
 [Eliminare utenti o gruppi &#40;Master Data Services&#41;](../master-data-services/delete-users-or-groups-master-data-services.md)   
 [Testare le autorizzazioni di un utente &#40;Master Data Services&#41;](../master-data-services/test-a-user-s-permissions-master-data-services.md)  
  
  
