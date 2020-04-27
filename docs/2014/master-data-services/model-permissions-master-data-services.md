---
title: Autorizzazioni per i modelli (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], permissions
- permissions [Master Data Services], models
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 733827ecace64ef86b54831f63fd8c2889203919
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65478959"
---
# <a name="model-permissions-master-data-services"></a>Autorizzazioni per i modelli (Master Data Services)
  Le autorizzazioni per i modelli si applicano a tutte le entità, alle gerarchie derivate, alle gerarchie esplicite e alle raccolte esistenti all'interno del modello. È possibile eseguire l'override delle autorizzazioni assegnate al modello per qualsiasi singolo oggetto.  
  
> [!NOTE]  
>  Se un utente è un amministratore di modelli, il modello viene visualizzato in tutte le aree funzionali dell'interfaccia utente. In caso contrario, il modello viene visualizzato solo nell'area funzionale **Visualizzatore** . Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
|Autorizzazione|Descrizione|  
|----------------|-----------------|  
|**Sola lettura**|In **Esplora**viene visualizzato il modello, ma l'utente non può aggiungere o rimuovere membri né aggiornare i valori degli attributi, le appartenenze a gerarchie o le appartenenze alla raccolta.|  
|**Aggiornamento**|In **Esplora**viene visualizzato il modello e l'utente può aggiungere e rimuovere membri, può aggiornare i valori degli attributi, le appartenenze alla gerarchia e le appartenenze alla raccolta.|  
|**Negare**|Il modello non viene visualizzato.|  
  
 Quando si assegna un'autorizzazione a un modello, l'utente ottiene l'accesso a tutte le versioni del modello. Non è possibile assegnare un'autorizzazione a una determinata versione.  
  
## <a name="see-also"></a>Vedi anche  
 [Assegnare autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Autorizzazioni per le entità &#40;Master Data Services&#41;](../../2014/master-data-services/entity-permissions-master-data-services.md)   
 [Autorizzazioni per raccolte &#40;Master Data Services&#41;](../../2014/master-data-services/collection-permissions-master-data-services.md)  
  
  
