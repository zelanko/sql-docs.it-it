---
title: Eliminare utenti o gruppi (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting groups [Master Data Services]
- groups [Master Data Services], deleting
- users [Master Data Services], deleting
- deleting users [Master Data Services]
ms.assetid: 0bbf9d2c-b826-48bb-8aa9-9905db6e717f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0114aa3ca6f6744303c3053003a622185d33f547
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479905"
---
# <a name="delete-users-or-groups-master-data-services"></a>Eliminare utenti o gruppi (Master Data Services)
  Eliminare utenti o gruppi se non si desidera più che accedano a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Prestare attenzione al seguente comportamento quando si eliminano utenti e gruppi:  
  
-   Se si elimina un utente membro di un gruppo che ha accesso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], l'utente potrà continuare ad accedere a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] finché non verrà rimosso dal gruppo Active Directory o locale.  
  
-   Se si elimina un gruppo, tutti gli utenti del gruppo che hanno effettuato l'accesso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] verranno visualizzati nell'elenco **Utenti** finché non verranno eliminati.  
  
-   Le modifiche alla sicurezza non vengono propagate a MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] per 20 minuti.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Autorizzazioni utenti e gruppi** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-delete-users-or-groups"></a>Per eliminare utenti o gruppi  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Autorizzazioni utenti e gruppi**.  
  
2.  Per eliminare un utente, rimanere nella pagina **Utenti** . Per eliminare un gruppo, dalla barra dei menu fare clic su **Gestisci gruppi**.  
  
3.  Nella griglia selezionare la riga relativa all'utente o al gruppo che si vuole eliminare.  
  
4.  Fare clic su **Elimina utente selezionato** o **Elimina gruppo selezionato**.  
  
5.  Nella finestra di dialogo di conferma fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza &#40;Master Data Services&#41;](../../2014/master-data-services/security-master-data-services.md)  
  
  
