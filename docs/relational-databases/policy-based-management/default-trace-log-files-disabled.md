---
title: File dei log di traccia predefiniti disabilitati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c27761e6-75ed-4ee4-a236-0cbc42e500a1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1407f55e2edab15768fb10288b78dd59ff93ddd1
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67940491"
---
# <a name="default-trace-log-files-disabled"></a>File dei log di traccia predefiniti disabilitati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questa regola consente di controllare il valore dell'opzione default trace enabled per la stored procedure sp_configure per determinare se la traccia predefinita sia impostata su ON (1) o OFF (0). Quando questa opzione è abilitata, la sessione di traccia predefinita fornisce informazioni sulla configurazione del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e sulle modifiche a esso apportate. In alcuni casi, queste informazioni possono essere utili per gli utenti e per il Servizio Supporto Tecnico Clienti [!INCLUDE[msCoName](../../includes/msconame-md.md)] durante la risoluzione dei problemi relativi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Utilizzare la stored procedure sp_configure per abilitare la traccia impostando il valore di default trace enabled su 1.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
