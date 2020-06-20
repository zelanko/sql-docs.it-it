---
title: Aumentare o disabilitare l'opzione blocked process threshold | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7983d9b7513a44b45311835be85c33fbc9b31397
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063861"
---
# <a name="increase-or-disable-blocked-process-threshold"></a>Aumento o disabilitazione dell'opzione blocked process threshold
  Queste regole consentono di controllare che l'opzione blocked process threshold sia impostata su 0, o disabilitata, o su un valore maggiore o uguale a 5 (secondi). L'impostazione dell'opzione blocked process threshold su un valore compreso tra 1 e 4 comporta l'esecuzione continua del monitoraggio deadlock. È consigliabile utilizzare i valori compresi tra 1 e 4 solo per la risoluzione dei problemi e mai a lungo termine o in un ambiente di produzione senza l'assistenza del Servizio Supporto Tecnico Clienti [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Per risolvere questo problema, impostare l'opzione blocked process threshold su un valore maggiore o uguale a 5 oppure su 0 per disabilitarla. Per impostare l'opzione su un valore di `5` secondi, eseguire l'istruzione seguente:  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 5 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Opzione di configurazione del server blocked process threshold](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
