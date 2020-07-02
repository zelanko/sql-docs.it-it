---
title: Autorizzazioni per i modelli
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], permissions
- permissions [Master Data Services], models
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 36e2b4cacd6636b2580aff1d8c27ea5a3a444906
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813248"
---
# <a name="model-permissions-master-data-services"></a>Autorizzazioni per i modelli (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Le autorizzazioni per i modelli si applicano a tutte le entità, alle gerarchie derivate, alle gerarchie esplicite e alle raccolte esistenti all'interno del modello. È possibile eseguire l'override delle autorizzazioni assegnate al modello per qualsiasi singolo oggetto.  
  
> [!NOTE]  
>  Se un utente è un amministratore di modelli, il modello viene visualizzato in tutte le aree funzionali dell'interfaccia utente. In caso contrario, il modello viene visualizzato solo nell'area funzionale **Visualizzatore** . Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
|Autorizzazione|Descrizione|  
|----------------|-----------------|  
|**Lettura**|L'utente può leggere i membri, gli attributi, le appartenenze a gerarchie o le appartenenze a raccolte.|  
|**Creare**|L'utente può creare i membri e assegnare i valori di attributo durante la creazione.|  
|**Update**|L'utente può aggiornare i membri, gli attributi, le appartenenze a gerarchie o le appartenenze a raccolte.|  
|**Eliminazione**|L'utente può eliminare i membri|  
|**Nega**|Negare l'accesso al modello|  
|**Admin**|Autorizzazione dell'amministratore per il modello. L'autorizzazione di amministratore è disponibile solo al livello del modello.|  
  
 Le autorizzazioni di lettura, creazione, aggiornamento ed eliminazione possono essere combinate. Quando vengono assegnate le autorizzazioni di creazione, aggiornamento ed eliminazione, l'autorizzazione di lettura viene assegnata automaticamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Assegnare autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Autorizzazioni per le entità &#40;Master Data Services&#41;](../master-data-services/entity-permissions-master-data-services.md)   
 [Autorizzazioni per raccolte &#40;Master Data Services&#41;](../master-data-services/collection-permissions-master-data-services.md)  
  
  
