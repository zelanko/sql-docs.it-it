---
title: Opzione di configurazione del server lightweight pooling | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default lightweight pooling
- decreasing overhead
- lightweight pooling option
- system overhead [SQL Server]
- performance [SQL Server], lightweight pooling
- context switching [SQL Server], lightweight pooling option
- excessive context switching [SQL Server]
- reducing overhead
- overhead [SQL Server]
ms.assetid: 2dc11b61-d065-4126-8e00-acf40390f9fb
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5d18b51a3868534089c88dc1c951148711e0d0c4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998033"
---
# <a name="lightweight-pooling-server-configuration-option"></a>Opzione di configurazione del server lightweight pooling
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'opzione **lightweight pooling** consente di ridurre l'overhead del sistema associato a un'eccessiva attività di scambio del contesto che talvolta si riscontra negli ambienti SMP (multiprocessori simmetrici, Symmetric Multiprocessor). Quando si verifica un'eccessiva attività di cambio del contesto, l'opzione lightweight pooling può assicurare una migliore velocità effettiva eseguendo direttamente il cambio del contesto e quindi riducendo le transizioni utente/kernel ring.  
  
 La modalità fiber viene utilizzata in situazioni specifiche in cui il cambio di contesto dei thread di lavoro UMS costituisce un collo di bottiglia critico per le prestazioni. Poiché questa situazione è poco frequente, la modalità fiber consente raramente di ottimizzare le prestazioni o la scalabilità in un sistema tipico. I miglioramenti apportati al cambio di contesto in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] hanno anche ridotto la necessità di usare la modalità fiber. Si consiglia di non utilizzare la modalità fiber per la pianificazione dell'operazione di routine. in quanto la modalità può ridurre le prestazioni eliminando i normali vantaggi del cambio del contesto e perché alcuni componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che utilizzano TLS (Thread Local Storage) oppure oggetti di proprietà del thread, ad esempio mutex (un tipo di oggetto del kernel di Win32), non funzionano correttamente in modalità fiber.  
  
 Se si imposta l'opzione **lightweight pooling** su 1, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene attivata la pianificazione in modalità fiber. Il valore predefinito dell'opzione è 0.  
  
 L'opzione **lightweight pooling** è un'opzione avanzata. Se si utilizza la stored procedure di sistema **sp_configure** per modificare l'impostazione, è possibile modificare **lightweight pooling** solo quando il valore di **show advanced options** è impostato su 1. L'impostazione diventa effettiva dopo il riavvio del server.  
  
> [!NOTE]  
>  Il lightweight pooling non è supportato per [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 e [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows XP. [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] fornisce supporto completo per il lightweight pooling.  
  
> [!NOTE]  
>  L'esecuzione di CLR (Common Language Runtime) non è supportata nell'ambito dell'opzione lightweight pooling. Disabilitare una delle due opzioni tra "clr enabled" e "lightweight pooling". Le caratteristiche che si basano su CLR e che non funzionano correttamente in modalità fiber includono il tipo di dati hierarchy, la replica e la gestione basata su criteri.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzione di configurazione del server clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opzione di configurazione del server clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)  
  
  
