---
title: Eliminare le autorizzazioni dei membri della gerarchia (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting member permissions [Master Data Services]
- members [Master Data Services], deleting permissions
- permissions [Master Data Services], deleting member permissions
ms.assetid: 7f22d5e2-70c1-422c-99c2-e995a47d812a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1562bc5d71bdf873c7be1f01a1dbf48fe85c05a5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84950549"
---
# <a name="delete-hierarchy-member-permissions-master-data-services"></a>Eliminare le autorizzazioni membri gerarchia (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eliminare le autorizzazioni dell'oggetto modello per rimuovere qualsiasi assegnazione attribuita.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Autorizzazioni utenti e gruppi** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-delete-hierarchy-member-permissions"></a>Per eliminare le autorizzazioni membri gerarchia  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Autorizzazioni utenti e gruppi**.  
  
2.  Nella pagina **Utenti** o **Gruppi** selezionare la riga relativa all'utente o al gruppo che si desidera modificare.  
  
3.  Fare clic su **Modifica utente selezionato**.  
  
4.  Fare clic sulla scheda **Membri gerarchia** .  
  
5.  Selezionare un modello dall'elenco **Modello** .  
  
6.  Selezionare una versione dall'elenco **Versione** .  
  
7.  Nel riquadro **Riepilogo autorizzazioni membri gerarchia** selezionare la riga relativa all'autorizzazione che si desidera eliminare.  
  
8.  Fare clic su **Elimina autorizzazione selezionata**.  
  
    > [!NOTE]  
    >  Se l'autorizzazione viene ereditata da un gruppo, non sarà possibile rimuoverla da un utente. È necessario invece rimuovere l'autorizzazione dal gruppo.  
  
## <a name="see-also"></a>Vedere anche  
 [Autorizzazioni membri gerarchia &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Assegnare autorizzazioni membri gerarchia &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
  
