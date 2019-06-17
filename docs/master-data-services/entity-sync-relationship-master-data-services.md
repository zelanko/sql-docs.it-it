---
title: Relazione di sincronizzazione delle entità (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: bd627a2d-dc64-47e9-9a71-2d0ad04b4962
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 30864765a61bfc0175fba06d54eebaea43b6baaf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483929"
---
# <a name="entity-sync-relationship-master-data-services"></a>Relazione di sincronizzazione delle entità (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  La sincronizzazione delle entità è una sincronizzazione unidirezionale e ripetibile tra le versioni dell'entità. Consente di condividere i dati dell'entità tra i vari modelli. È possibile mantenere un'unica origine in un modello e riusare questi dati master in altri modelli. Ad esempio, è possibile archiviare i dati sullo stato per gli Stati Uniti in un'entità di modello e riusare i dati in altri modelli.  
  
 Con la sincronizzazione delle entità, è anche possibile eseguire una copia occasionale dei dati.  
  
 Tutti i membri foglia con attributi di file e in formato libero nell'entità di origine sono sincronizzati con l'entità di destinazione durante la sincronizzazione. In questo modo vengono creati, eliminati e modificati i membri e lo schema dell'entità.  
  
 Dopo aver stabilito una relazione di sincronizzazione, l'entità di destinazione può essere modificata solo dal processo di sincronizzazione. Una relazione di sincronizzazione può essere rimossa in qualsiasi momento per rendere modificabile l'entità di destinazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare ed eseguire una relazione di sincronizzazione delle entità &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [Modificare ed eliminare una relazione di sincronizzazione delle entità &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
