---
title: Opzione di configurazione del server server trigger recursion | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- recursive triggers [SQL Server]
- triggers [SQL Server], recursive
- server trigger recursion option
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f1fc67db5d7d62c9257f6d66359b0166b6ed8c0b
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640682"
---
# <a name="server-trigger-recursion-server-configuration-option"></a>Opzione di configurazione del server server trigger recursion
  L'opzione **server trigger recursion** consente di specificare se consentire o meno l'attivazione ricorsiva di trigger a livello del server. Se l'opzione è impostata su 1 (ON), i trigger a livello del server possono essere attivati in modo ricorsivo. Se è impostata su 0 (OFF ), i trigger non possono essere attivati in modo ricorsivo. Con questa impostazione viene impedita solo la ricorsione diretta. Per disabilitare anche la ricorsione indiretta, impostare l'opzione **nested triggers** su 0. Il valore predefinito è 1 (ON). L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
 Per altre informazioni, vedere [Creazione di trigger annidati](../../relational-databases/triggers/create-nested-triggers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
