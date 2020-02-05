---
title: Aumentare o disabilitare l'opzione blocked process threshold | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ef493b3af967adf83b59a1d272f69b0b677149c5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68087226"
---
# <a name="increase-or-disable-blocked-process-threshold"></a>Aumento o disabilitazione dell'opzione blocked process threshold
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
