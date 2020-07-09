---
title: Piano di manutenzione (Gestisci connessioni) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.connections.f1
ms.assetid: 95ad9375-6584-423e-b9de-0e86782f8017
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 495ec4a69d960cfec8534b37490b10fe66c5934d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754547"
---
# <a name="maintenance-plan-manage-connections"></a>Piano di manutenzione (Gestisci connessioni)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Utilizzare la finestra di dialogo **Gestisci connessioni** per specificare le proprietà delle connessioni utilizzate dai piani di manutenzione. Quando si crea un piano di manutenzione viene creata una connessione locale al server in cui è stato creato il piano. Utilizzare questa connessione per creare le attività che vengono eseguite nella connessione locale. Se richiesto, utilizzare la finestra di dialogo **Gestisci connessioni** per aggiungerle. Le connessioni aggiuntive configurate vengono visualizzate nella casella delle connessioni di ogni attività.  
  
## <a name="options"></a>Opzioni  
 **Server**  
 Istanza del server.  
  
 **autenticazione**  
 Indica se la connessione utilizza l'autenticazione di Windows oppure l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

> [!IMPORTANT]  
> Il pacchetto è archiviato nel database **msdb** insieme al relativo set **ProtectionLevel** impostato su **ServerStorage**. In questo modo, se si usa l'*autenticazione di SQL Server*, la password non sarà crittografata in **msdb**. È possibile usare l'*autenticazione di SQL Server* purché il database **msdb** sia protetto. È tuttavia consigliabile usare l'*autenticazione di Windows*

## <a name="see-also"></a>Vedere anche  
 [Piani di manutenzione](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
