---
title: Correggi la maschera di affinità e la maschera di output di input affinità | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3139c864805c7df9220afc9b81d2a242775f4fa7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62856704"
---
# <a name="correct-affinity-mask-and-affinity-input-output-mask-overlap"></a>Correzione della sovrapposizione della maschera di affinità e della maschera di output di input affinità
  Questa regola consente di controllare se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone di uno o più processori a cui sono assegnate sia l'opzione affinity mask sia l'opzione affinity I/O mask. In un computer con più di un processore, le opzioni affinity mask e affinity I/O mask vengono utilizzate per designare le CPU utilizzate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'abilitazione di una CPU con entrambe le opzioni può ridurre le prestazioni forzando un utilizzo eccessivo del processore.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 È consigliabile specificare entrambe le opzioni, affinity mask e affinity I/O mask, ma abilitarne una sola per volta per ciascuna CPU.  
  
 Non abilitare entrambe le opzioni per la stessa CPU. I bit corrispondenti a ogni CPU devono essere associati a uno dei tre stati seguenti:  
  
-   0 sia nell'opzione affinity mask sia nell'opzione affinity I/O mask  
  
-   0 nell'opzione affinity mask e 1 nell'opzione affinity I/O mask  
  
-   1 nell'opzione affinity mask e 0 nell'opzione affinity I/O mask  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Opzione di configurazione del server affinity mask](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)  
  
 [Opzione di configurazione del server Affinity Mask I/O](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)  
  
 [Opzione di configurazione affinity64 mask](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)  
  
 [Opzione di configurazione del server Affinity64 I/O](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
