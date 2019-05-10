---
title: Consolidare le autorizzazioni (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], consolidated member attribute permissions
- consolidated members [Master Data Services], attribute permissions
- permissions [Master Data Services], consolidated members
- members [Master Data Services], consolidated member permissions
ms.assetid: 084055a3-5fd3-43f3-b620-ac6afab42a3d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 86b20b7bbe0e9cf95805dd859c3c85bab60b61a9
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483498"
---
# <a name="consolidated-permissions-master-data-services"></a>Autorizzazioni consolidate (Master Data Services)
  Le autorizzazioni consolidate si applicano ai valori di attributo per tutti i membri consolidati di un'entità.  
  
 Le autorizzazioni consolidate si applicano solo alle entità abilitate per gerarchie esplicite e raccolte.  
  
 **Note:**  
  
-   Le autorizzazioni foglia si applicano solo all'area funzionale **Visualizzatore** dell'interfaccia utente.  
  
-   Le autorizzazioni assegnate agli attributi **Name** e **Code** non sono applicate.  
  
|Autorizzazione|Descrizione|  
|----------------|-----------------|  
|**Sola lettura**|I membri consolidati vengono visualizzati, ma l'utente non può aggiungerli, rimuoverli o modificarli.|  
|**Update**|I membri consolidati vengono visualizzati e l'utente può aggiungerli, rimuoverli e modificarli.|  
|**Nega**|I membri consolidati per l'entità non vengono visualizzati.|  
  
## <a name="attribute-permissions"></a>Autorizzazioni per attributi  
 Le autorizzazioni per gli attributi si applicano ai valori degli attributi per l'entità specifica. Gli utenti che dispongono solo delle autorizzazioni per gli attributi non possono aggiungere o rimuovere membri.  
  
|Autorizzazione|Descrizione|  
|----------------|-----------------|  
|**Sola lettura**|L'attributo viene visualizzato, ma l'utente non può modificare i valori di attributo.|  
|**Update**|L'attributo viene visualizzato e l'utente può modificare i valori di attributo.|  
|**Nega**|L'attributo non viene visualizzato.<br /><br /> Nota: È possibile negare in modo esplicito l'accesso agli attributi Name e Code.|  
  
## <a name="see-also"></a>Vedere anche  
 [Assegnare autorizzazioni per oggetti modello &#40;Master Data Services&#41;](assign-model-object-permissions-master-data-services.md)   
 [Autorizzazioni per elementi foglia &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [Autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Membri &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Attributi &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
