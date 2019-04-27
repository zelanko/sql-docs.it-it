---
title: Opzione di configurazione del server ft notify bandwidth | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- ft notify bandwidth opion
- small memory buffers
- memory [SQL Server], buffers
ms.assetid: 9ca284c5-f3e0-4a67-a132-fff376ff0ffe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 375e7c8a1bb520f5a3004c5279682d5b3f145b13
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62782496"
---
# <a name="ft-notify-bandwidth-server-configuration-option"></a>Opzione di configurazione del server ft notify bandwidth
  L'opzione **ft notify bandwidth** consente di specificare la dimensione massima consentita per il pool di buffer di memoria di piccole dimensioni, ovvero dei buffer di memoria di 64 KB. Il valore del parametro *max* specifica il numero massimo di buffer che deve essere gestito in un pool di buffer di piccole dimensioni con lo strumento di gestione della memoria del servizio full-text. Se il `max` valore è zero, non esiste alcun limite al numero di buffer consentito in un pool di buffer di piccole dimensioni.  
  
 Il parametro **min** specifica il numero minimo di buffer di memoria che deve essere gestito nel pool di buffer di memoria di piccole dimensioni. In seguito alla richiesta dello strumento di gestione della memoria di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tutti i pool di buffer in eccesso vengono rilasciati, ma viene mantenuto il numero minimo di buffer. Tuttavia, se il valore **min** è uguale a zero, vengono rilasciati tutti i buffer di memoria.  
  
 In determinati casi il numero di buffer allocati risulta inferiore al valore specificato nel parametro **min** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Opzione di configurazione del server ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
