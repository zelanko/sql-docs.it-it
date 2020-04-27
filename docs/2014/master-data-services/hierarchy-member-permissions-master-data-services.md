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
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 371c7c605b5415654c01f3faa66fbd0801202785
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482957"
---
# <a name="hierarchy-member-permissions-master-data-services"></a>Autorizzazioni membri gerarchie (Master Data Services)
  Le autorizzazioni membri gerarchia sono facoltative e devono essere utilizzate solo quando si desidera che un utente abbia accesso limitato a membri specifici. Se non si assegnano autorizzazioni nella scheda **Membri gerarchia** , le autorizzazioni dell'utente sono basate esclusivamente su quelle assegnate nella scheda **Modelli** .  
  
 Le autorizzazioni dei [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] membri della gerarchia vengono assegnate nell'area funzionale **autorizzazioni utenti e gruppi** della scheda **membri gerarchia** nell'interfaccia utente (UI). Queste autorizzazioni determinano a quali membri può accedere un utente nell'area funzionale **Esplora** dell'interfaccia utente.  
  
 Nella scheda **Membri gerarchia** ogni gerarchia è rappresentata come albero. Quando si assegna un'autorizzazione a un nodo dell'albero, tutti i figli la ereditano, a meno che non sia stato assegnata in modo esplicito a un livello inferiore.  
  
> [!NOTE]  
>  Quando si assegna un'autorizzazione a un nodo di una gerarchia, a tutti i membri inclusi negli altri nodi dello stesso livello o di un livello superiore l'autorizzazione viene negata.  
  
 In **Esplora**le autorizzazioni per i membri vengono applicate in tutte le posizioni in cui il membro viene visualizzato. Un membro con autorizzazione di sola **lettura** , ad esempio, è di sola lettura in tutte le entità, gerarchie e raccolte a cui appartiene.  
  
 Le autorizzazioni membri gerarchia si applicano alla versione del modello cui sono assegnate e a eventuali copie future della versione. Non si applicano a versioni precedenti a quella a cui sono assegnate.  
  
|Autorizzazione|Descrizione|  
|----------------|-----------------|  
|**Sola lettura**|I membri vengono visualizzati, ma l'utente non può modificarli. L'utente non può inoltre spostare i membri in qualsiasi gerarchia o raccolta esplicita cui essi appartengono.<br /><br /> Nota: se si assegna l'autorizzazione di sola **lettura** a **root**, i membri nella **radice** sono di sola lettura. nelle gerarchie esplicite e nelle raccolte, tuttavia, l'utente può spostare i membri nella **radice** e aggiungere nuovi membri alla **radice**.|  
|**Aggiornamento**|I membri vengono visualizzati e l'utente può modificarli. L'utente può inoltre spostare i membri in qualsiasi gerarchia o raccolta esplicita cui essi appartengono.|  
|**Negare**|I membri non vengono visualizzati.|  
  
 Nella scheda **Membri gerarchia** le autorizzazioni assegnate non vengono applicate immediatamente. La frequenza con cui le autorizzazioni vengono applicate dipende dall'**impostazione relativa all'intervallo di elaborazione della sicurezza dei membri** nella tabella Impostazioni sistema del database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . È possibile applicare immediatamente autorizzazioni di membri seguendo i passaggi descritti in [Applicare immediatamente autorizzazioni membri &#40;Master Data Services&#41;](immediately-apply-member-permissions-master-data-services.md).  
  
> [!NOTE]  
>  Non è possibile assegnare autorizzazioni membri gerarchie a gerarchie ricorsive, gerarchie derivate con estremità esplicite e a gerarchie derivate con livelli nascosti.  
  
## <a name="possible-overlapping-permissions"></a>Possibili autorizzazioni sovrapposte  
 Quando si assegnano autorizzazioni ai membri, è possibile che sia necessario risolvere eventuali autorizzazioni sovrapposte.  
  
### <a name="when-a-member-belongs-to-multiple-hierarchies"></a>Quando un membro appartiene a più gerarchie  
 Due o più gerarchie possono contenere lo stesso membro.  
  
-   Se a un nodo della gerarchia viene assegnata l'autorizzazione **aggiornamento** e a un altro viene assegnata l'autorizzazione di sola **lettura**, i membri del nodo sono di sola **lettura**.  
  
-   Se a un nodo della gerarchia viene assegnata l'autorizzazione **aggiornamento** o sola **lettura** e a un altro nodo viene assegnata l'autorizzazione **Nega**, i membri del nodo non verranno visualizzati.  
  
## <a name="see-also"></a>Vedi anche  
 [Assegnare autorizzazioni membri gerarchia &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Modalità di determinazione delle autorizzazioni &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Membri &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Gerarchie &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchies-master-data-services.md)   
 [Applicare immediatamente autorizzazioni membri &#40;Master Data Services&#41;](immediately-apply-member-permissions-master-data-services.md)  
  
  
