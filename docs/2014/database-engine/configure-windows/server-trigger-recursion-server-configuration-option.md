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
ms.openlocfilehash: 23a4997bd1a6f8b2c04af34d5cdc3229575901a9
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934853"
---
# <a name="server-trigger-recursion-server-configuration-option"></a>Opzione di configurazione del server server trigger recursion
  L'opzione **server trigger recursion** consente di specificare se consentire o meno l'attivazione ricorsiva di trigger a livello del server. Se l'opzione è impostata su 1 (ON), i trigger a livello del server possono essere attivati in modo ricorsivo. Se è impostata su 0 (OFF ), i trigger non possono essere attivati in modo ricorsivo. Con questa impostazione viene impedita solo la ricorsione diretta. Per disabilitare anche la ricorsione indiretta, impostare l'opzione **nested triggers** su 0. Il valore predefinito è 1 (ON). L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
 Per altre informazioni, vedere [Creazione di trigger annidati](../../relational-databases/triggers/create-nested-triggers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
