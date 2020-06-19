---
title: Opzione di configurazione del server allow updates | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d7e3ede317509a2044be90635db46e30a932af66
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935912"
---
# <a name="allow-updates-server-configuration-option"></a>Opzione di configurazione del server allow updates
  Questa opzione è ancora presente nella stored procedure **sp_configure** , sebbene la relativa funzionalità non sia disponibile in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'impostazione non ha alcun effetto. Gli aggiornamenti diretti delle tabelle di sistema non sono supportati.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 La modifica dell'opzione **allow updates** provocherà l'esito negativo dell'istruzione RECONFIGURE. È necessario eliminare le modifiche apportate all'opzione **allow updates** in tutti gli script.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
