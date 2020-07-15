---
title: Opzione di configurazione del server ft crawl bandwidth | Microsoft Docs
description: Informazioni sull'opzione "ft crawl bandwidth". Scoprire come influisce sul numero di buffer mantenuti da SQL Server nel pool di buffer di memoria di grandi dimensioni.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- large memory buffers
- memory [SQL Server], buffers
- ft crawl bandwidth option
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 59caa1e868c4caab24afd17909c34f57c96f0005
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789788"
---
# <a name="ft-crawl-bandwidth-server-configuration-option"></a>Opzione di configurazione del server ft crawl bandwidth
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  L'opzione **ft crawl bandwidth** consente di specificare la dimensione massima consentita per il pool di buffer di memoria di grandi dimensioni, ovvero dei buffer di memoria di 4 MB. Il valore del parametro **max** specifica il numero massimo di buffer che deve essere gestito in un pool di buffer di grandi dimensioni tramite lo strumento di gestione della memoria del servizio full-text. Se il valore **max** è uguale a zero, non esiste alcuna limitazione per il numero massimo di buffer consentito in un pool di buffer di grandi dimensioni.  
  
 Il parametro **min** specifica il numero minimo di buffer di memoria che deve essere gestito nel pool di buffer di memoria di grandi dimensioni. In seguito alla richiesta dello strumento di gestione della memoria di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tutti i pool di buffer in eccesso vengono rilasciati, ma viene mantenuto il numero minimo di buffer. Tuttavia, se il valore **min** è uguale a zero, vengono rilasciati tutti i buffer di memoria.  
  
 In determinati casi il numero di buffer allocati risulta inferiore al valore specificato nel parametro **min** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Opzione di configurazione del server ft notify bandwidth](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
