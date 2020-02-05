---
title: Opzione di configurazione del server allow updates | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3cccccebcbbd9054752aa8aa4e65f3f2bc17b342
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68013155"
---
# <a name="allow-updates-server-configuration-option"></a>Opzione di configurazione del server allow updates
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Questa opzione è ancora presente nella stored procedure **sp_configure** , sebbene la relativa funzionalità non sia disponibile in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'impostazione non ha alcun effetto. Gli aggiornamenti diretti delle tabelle di sistema non sono supportati.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 La modifica dell'opzione **allow updates** provocherà l'esito negativo dell'istruzione RECONFIGURE. È necessario eliminare le modifiche apportate all'opzione **allow updates** in tutti gli script.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
