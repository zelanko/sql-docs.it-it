---
title: Criteri di correzione della sovrapposizione delle opzioni affinity mask e affinity I/O mask
description: Informazioni su come abilitare criteri che controllano se a un'istanza di SQL Server sono assegnati uno o più processori per l'uso con entrambe le opzioni affinity mask e affinity I/O mask per la gestione basata su criteri in SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b225710aaadf3ea605e3cffd91a5a4fea2a51e62
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557796"
---
# <a name="correct-affinity-mask-and-affinity-input-and-output-mask-overlap"></a>Correggere la sovrapposizione delle opzioni affinity mask e affinity I/O mask
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
