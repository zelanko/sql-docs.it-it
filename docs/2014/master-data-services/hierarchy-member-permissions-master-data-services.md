---
title: Autorizzazioni dei membri della gerarchia (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], permissions
- permissions [Master Data Services], members
ms.assetid: b3880eed-1bf6-4f65-ab23-b08c194cc858
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a7e762a450a28f1d07e58a0baa6f7f3ff3948681
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62924386"
---
# <a name="hierarchy-member-permissions-master-data-services"></a>Autorizzazioni membri gerarchie (Master Data Services)
  Le autorizzazioni membri gerarchia sono facoltative e devono essere utilizzate solo quando si desidera che un utente abbia accesso limitato a membri specifici. Se non si assegnano autorizzazioni nella scheda **Membri gerarchia** , le autorizzazioni dell'utente sono basate esclusivamente su quelle assegnate nella scheda **Modelli** .  
  
 Le autorizzazioni dei membri della gerarchia vengono assegnate nell'area funzionale [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Autorizzazioni utenti e gruppi **della scheda** Membri gerarchia **nell'interfaccia utente di** . Queste autorizzazioni determinano a quali membri può accedere un utente nell'area funzionale **Esplora** dell'interfaccia utente.  
  
 Nella scheda **Membri gerarchia** ogni gerarchia è rappresentata come albero. Quando si assegna un'autorizzazione a un nodo dell'albero, tutti i figli la ereditano, a meno che non sia stato assegnata in modo esplicito a un livello inferiore.  
  
> [!NOTE]  
>  Quando si assegna un'autorizzazione a un nodo di una gerarchia, a tutti i membri inclusi negli altri nodi dello stesso livello o di un livello superiore l'autorizzazione viene negata.  
  
 In **Esplora**le autorizzazioni per i membri vengono applicate in tutte le posizioni in cui il membro viene visualizzato. Ad esempio, un membro con **Read-only** l'autorizzazione è di sola lettura in qualsiasi entità, gerarchie e raccolte alle quali appartiene.  
  
 Le autorizzazioni membri gerarchia si applicano alla versione del modello cui sono assegnate e a eventuali copie future della versione. Non si applicano a versioni precedenti a quella a cui sono assegnate.  
  
|Autorizzazione|Descrizione|  
|----------------|-----------------|  
|**Sola lettura**|I membri vengono visualizzati, ma l'utente non può modificarli. L'utente non può inoltre spostare i membri in qualsiasi gerarchia o raccolta esplicita cui essi appartengono.<br /><br /> Nota: Se si assegnano **Read-only** l'autorizzazione per **radice**, i membri in **radice** sono di sola lettura; nelle gerarchie esplicite e raccolte, tuttavia, l'utente può spostarsi ai membri di **Radice** e aggiungere nuovi membri a **radice**.|  
|**Update**|I membri vengono visualizzati e l'utente può modificarli. L'utente può inoltre spostare i membri in qualsiasi gerarchia o raccolta esplicita cui essi appartengono.|  
|**Nega**|I membri non vengono visualizzati.|  
  
 Nella scheda **Membri gerarchia** le autorizzazioni assegnate non vengono applicate immediatamente. La frequenza con cui le autorizzazioni vengono applicate dipende dall'**impostazione relativa all'intervallo di elaborazione della sicurezza dei membri** nella tabella Impostazioni sistema del database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . È possibile applicare immediatamente autorizzazioni di membri seguendo i passaggi descritti in [Immediately Apply Member Permissions &#40;Master Data Services&#41;](immediately-apply-member-permissions-master-data-services.md).  
  
> [!NOTE]  
>  Non è possibile assegnare autorizzazioni membri gerarchie a gerarchie ricorsive, gerarchie derivate con estremità esplicite e a gerarchie derivate con livelli nascosti.  
  
## <a name="possible-overlapping-permissions"></a>Possibili autorizzazioni sovrapposte  
 Quando si assegnano autorizzazioni ai membri, è possibile che sia necessario risolvere eventuali autorizzazioni sovrapposte.  
  
### <a name="when-a-member-belongs-to-multiple-hierarchies"></a>Quando un membro appartiene a più gerarchie  
 Due o più gerarchie possono contenere lo stesso membro.  
  
-   Se un nodo della gerarchia viene assegnato **Update** viene assegnata l'autorizzazione e l'altra **Read-only**, i membri nel nodo **Read-only**.  
  
-   Se un nodo della gerarchia viene assegnato **Update** oppure **Read-only** è assegnata l'autorizzazione e un altro nodo **Deny**, quindi non vengono visualizzati i membri nel nodo.  
  
## <a name="see-also"></a>Vedere anche  
 [Assegnare autorizzazioni membri gerarchia &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Modalità di determinazione delle autorizzazioni &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Membri &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Gerarchie &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchies-master-data-services.md)   
 [Applicare immediatamente autorizzazioni membri &#40;Master Data Services&#41;](immediately-apply-member-permissions-master-data-services.md)  
  
  
