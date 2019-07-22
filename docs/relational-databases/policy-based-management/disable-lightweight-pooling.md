---
title: Disabilitare l'opzione lightweight pooling | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 481bb43d-6fe5-497c-9096-971fb6bf733b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 155426b05311354153e03994f854f3860afad9c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940446"
---
# <a name="disable-lightweight-pooling"></a>Disabilitazione di lightweight pooling
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questa regola consente di controllare che l'opzione lightweight pooling sia disabilitata nel server. Se si imposta lightweight pooling su 1, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] passerà alla pianificazione in modalità fiber. La modalità fiber deve essere utilizzata in situazioni specifiche in cui il cambio di contesto dei thread di lavoro UMS costituisce un importante collo di bottiglia per le prestazioni. Poiché questa situazione è poco frequente, la modalità fiber consente raramente di ottimizzare le prestazioni o la scalabilità in un sistema tipico.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 L'opzione lightweightpooling deve essere abilitata solo in seguito a test approfonditi, dopo avere valutato tutte le altre possibilità di ottimizzazione delle prestazioni, e quando il cambio del contesto è un problema noto nell'ambiente.  
  
 È consigliabile evitare di utilizzare la pianificazione in modalità fiber per operazioni di routine, in quanto può ridurre le prestazioni impedendo i normali vantaggi derivati dal cambio del contesto e perché alcuni componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che utilizzano TLS (Thread Local Storage) o oggetti di proprietà del thread, ad esempio i mutex (un tipo di oggetto kernel Win32), non possono funzionare correttamente in modalità fiber.  
  
 Per rimuovere l'opzione lightweight pooling, eseguire l'istruzione seguente, quindi riavviare il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
```sql  
sp_configure 'show advanced options', 1;  
GO  
sp_configure 'lightweight pooling', 0;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Opzione di configurazione del server lightweight pooling](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
