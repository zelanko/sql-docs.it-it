---
title: Autorizzazioni utenti e gruppi sovrapposte (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- users [Master Data Services], resolving permissions
- permissions [Master Data Services], user and group overlaps
- groups [Master Data Services], resolving permissions
ms.assetid: 31c3cf7d-17d4-4474-b6a7-ffcb9fc45b37
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6c3bdb745d836959f563d19dc9897b718a2c9b16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478880"
---
# <a name="overlapping-user-and-group-permissions-master-data-services"></a>Autorizzazioni utenti e gruppi sovrapposte (Master Data Services)
  Le autorizzazioni di un utente si basano su:  
  
-   Autorizzazioni ereditate dalle appartenenze a gruppi.  
  
-   Autorizzazioni assegnate in modo esplicito all'utente.  
  
 Se un utente è un membro di più gruppi e questi gruppi dispongono dell'accesso a Gestione dati master, si applicano le regole seguenti:  
  
-   **Nega** esegue l'override di tutte le altre autorizzazioni.  
  
-   **Aggiornamento** esegue l'override **di sola lettura**.  
  
 Queste regole si applicano a entrambe le schede **Modelli** e **Membri gerarchia** . Le autorizzazioni vengono risolte per ogni scheda e quindi combinate. Per altre informazioni, vedere [Modalità di determinazione delle autorizzazioni &#40;Master Data Services&#41;](how-permissions-are-determined-master-data-services.md).  
  
> [!NOTE]  
>  Nell'interfaccia utente è possibile visualizzare la risoluzione delle autorizzazioni di utenti e gruppi sovrapposte. Nelle schede **Modelli** e **Membri gerarchia** è presente un elenco a discesa da cui è possibile scegliere **Valide** per visualizzare le autorizzazioni valide.  
  
## <a name="example-1"></a>Esempio 1  
 ![mds_conc_user_group_ex_1](../../2014/master-data-services/media/mds-conc-user-group-ex-1.gif "mds_conc_user_group_ex_1")  
  
 L'utente appartiene al Gruppo 1 e al Gruppo 2.  
  
 L'utente dispone delle autorizzazioni di sola **lettura** per l'entità Product.  
  
 Il gruppo 1 ha l'autorizzazione **Update** per l'entità Product.  
  
 Il gruppo 2 dispone dell'autorizzazione di sola **lettura** per l'entità Product.  
  
 Risultato: l'autorizzazione valida dell'utente è **Update** per l'entità Product.  
  
## <a name="example-2"></a>Esempio 2  
 ![mds_conc_user_group_ex_2](../../2014/master-data-services/media/mds-conc-user-group-ex-2.gif "mds_conc_user_group_ex_2")  
  
 L'utente appartiene al Gruppo 1 e al Gruppo 2.  
  
 L'utente dispone delle autorizzazioni di sola **lettura** per l'entità Product.  
  
 Il gruppo 1 ha l'autorizzazione **Update** per l'entità Product.  
  
 Il gruppo 2 ha l'autorizzazione **Deny** per l'entità Product.  
  
 Risultato: l'autorizzazione valida dell'utente è **Deny** per l'entità Product.  
  
## <a name="example-3"></a>Esempio 3  
 ![mds_conc_user_group_ex_3](../../2014/master-data-services/media/mds-conc-user-group-ex-3.gif "mds_conc_user_group_ex_3")  
  
 L'utente appartiene al Gruppo 1 e al Gruppo 2.  
  
 L'utente dispone dell'autorizzazione **Update** per un gruppo di membri in un nodo gerarchia.  
  
 Il gruppo 1 dispone dell'autorizzazione di sola **lettura** per un gruppo di membri in un nodo della gerarchia.  
  
 Il gruppo 2 dispone dell'autorizzazione di sola **lettura** per un gruppo di membri in un nodo della gerarchia.  
  
 Risultato: l'autorizzazione utente valida è **Update** per i membri.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità di determinazione delle autorizzazioni &#40;Master Data Services&#41;](how-permissions-are-determined-master-data-services.md)   
 [Autorizzazioni per modelli e membri sovrapposte &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-model-and-member-permissions-master-data-services.md)  
  
  
