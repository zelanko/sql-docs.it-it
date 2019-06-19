---
title: Opzione di configurazione del server Affinity Mask I/O | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- affinity I/O mask option
- processor affinity [SQL Server]
- binding processors [SQL Server]
- CPU affinity mask option
ms.assetid: 9950a8c9-9fe0-4003-95df-6f0d1becb0e7
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: f8ddb88c264df2c1d2b3918994bf0ea8c81a3b4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66786890"
---
# <a name="affinity-input-output-mask-server-configuration-option"></a>Opzione di configurazione del server Affinity Mask I/O
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Per eseguire il multitasking, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows spostano talvolta thread di processo tra processori diversi. Nonostante dal punto di vista del sistema operativo questa attività sia efficiente, essa può ridurre le prestazioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con carichi di lavoro di sistema eccessivi perché i dati vengono caricati ripetutamente nella cache di ogni processore. In tali condizioni, l'assegnazione dei processori a specifici thread può aumentare le prestazioni eliminando il ricaricamento dei processori. Questa associazione tra un thread e un processore è definita affinità processori.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'affinità processori per mezzo di due opzioni affinity mask: **affinity mask** (nota anche come **CPU affinity mask**) e **affinity I/O mask**. Per altre informazioni sull'opzione **affinity mask** , vedere [Opzione di configurazione del server affinity mask](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md). Il supporto di CPU e Affinity I/O per server con 33 fino a 64 processori richiede rispettivamente l'uso aggiuntivo dell' [opzione di configurazione del server affinity64 mask](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) e dell' [opzione di configurazione del server affinity64 Input-Output mask](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md) .  
  
> [!NOTE]  
>  Il supporto dell'affinità nei server dotati di un numero di processori compreso tra 33 e 64 è disponibile solo su sistemi operativi a 64 bit.  
  
 L'opzione **affinity I/O mask** associa l'I/O su disco di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un subset specificato di CPU. Negli ambienti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di fascia alta con elaborazione delle transazioni online (OLTP), questa estensione può migliorare le prestazioni dei thread di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che generano operazioni di I/O. Questa funzionalità avanzata non supporta affinità hardware per singoli dischi o controller del disco.  
  
 Il valore di **affinity I/O mask** specifica quali CPU di un computer multiprocessore sono idonee a elaborare le operazioni di I/O su disco di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La maschera è costituita da una mappa di bit nella quale il primo bit a destra specifica la CPU di ordine inferiore (ovvero CPU(0)), il bit alla sua immediata sinistra specifica la CPU di ordine successivo (ovvero CPU(1)) e così via. Per configurare più di 32 processori, impostare sia l'opzione **affinity I/O mask** che l'opzione **affinity64 I/O mask**.  
  
 I valori di **affinity I/O mask** sono i seguenti:  
  
-   L'uso di una **affinity I/O mask** da 1 byte copre fino a 8 CPU in un computer multiprocessore.  
  
-   L'uso di una **affinity I/O mask** da 2 byte copre fino a 16 CPU in un computer multiprocessore.  
  
-   L'uso di una **affinity I/O mask** da 3 byte copre fino a 24 CPU in un computer multiprocessore.  
  
-   L'uso di una **affinity I/O mask** da 4 byte copre fino a 32 CPU in un computer multiprocessore.  
  
-   Per coprire più di 32 CPU, configurare una **affinity I/O mask** da 4 byte per le prime 32 CPU e una **affinity64 I/O mask** fino a 4 byte per le CPU rimanenti.  
  
 Un bit 1 nello schema della maschera di affinità di I/O indica che la CPU corrispondente è idonea all'esecuzione di operazioni di I/O su disco di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mentre un bit 0 indica che per la CPU corrispondente non deve essere pianificata alcuna operazione di I/O su disco di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando tutti i bit sono impostati su zero oppure l'opzione **affinity I/O mask** non è specificata, le operazioni di I/O su disco di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono pianificate per una qualsiasi CPU idonea a elaborare i thread di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 L'impostazione dell'opzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **affinity I/O mask** è un'attività complessa, che è consigliabile eseguire solo in caso di necessità. Nella maggior parte dei casi l'affinità predefinita di Windows 2000 o Windows Server 2003 garantisce livelli di prestazioni ottimali.  
  
 Quando si specifica l'opzione **affinity I/O mask** , è necessario usarla insieme all'opzione di configurazione **affinity mask** . Non abilitare la stessa CPU sia nell'opzione **affinity I/O mask** che nell'opzione **affinity mask** . I bit corrispondenti alle singole CPU devono rispettare uno dei tre stati seguenti:  
  
-   0 sia nell'opzione **affinity I/O mask** che nell'opzione **affinity mask** .  
  
-   1 nell'opzione **affinity I/O mask** e 0 nell'opzione **affinity mask** .  
  
-   0 nell'opzione **affinity I/O mask** e 1 nell'opzione **affinity mask** .  
  
 L'opzione **affinity I/O mask** è un'opzione avanzata. Se si usa la stored procedure di sistema **sp_configure** per modificare l'impostazione, è possibile modificare **affinity I/O mask** solo quando il valore di **show advanced options** è impostato su 1. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per riconfigurare l'opzione **affinity I/O mask** è necessario riavviare l'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!CAUTION]  
>  Non configurare l'affinità di CPU nel sistema operativo Windows e contemporaneamente l'opzione affinity mask in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le due impostazioni mirano a ottenere lo stesso risultato e, se le configurazioni sono incoerenti, potrebbero causare risultati imprevisti. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] La configurazione ottimale dell'affinità di CPU può essere ottenuta usando l'opzione **sp_configure** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
