---
title: '@@IO_BUSY (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@IO_BUSY'
- '@@IO_BUSY_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- ticks [SQL Server]
- I/O [SQL Server], time spent performing operations
- '@@IO_BUSY function'
- output operations [SQL Server]
- input operations [SQL Server]
- time [SQL Server], I/O operations
ms.assetid: 3c26770c-41ae-4e34-8c82-7bef920ffbca
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f7bb537df511483b05647d36dba2a0323e44b199
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68024266"
---
# <a name="x40x40io_busy-transact-sql"></a>&#x40;&#x40;IO_BUSY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce il periodo di tempo impiegato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'esecuzione di operazioni di input e di output dopo l'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il risultato è in incrementi di tempo di CPU, o "tick" ed è cumulativo per tutte le CPU, pertanto può essere maggiore del tempo trascorso effettivo. Per convertire in microsecondi, moltiplicare per @@TIMETICKS.  
  
> [!NOTE]  
>  Se il periodo di tempo restituito nelle variabili @@CPU_BUSY o @@IO_BUSY è superiore a circa 49 giorni di tempo cumulativo della CPU, si riceve un avviso di overflow aritmetico. In tal caso, il valore delle variabili @@CPU_BUSY, @@IO_BUSY e @@IDLE non è preciso.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
@@IO_BUSY  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **integer**  
  
## <a name="remarks"></a>Osservazioni  
 Per visualizzare un report contenente dati statistici relativi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eseguire la procedura sp_monitor.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il numero di millisecondi impiegati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'esecuzione di operazioni di input e di output tra l'ora di avvio e l'ora corrente. Per evitare un overflow aritmetico durante la conversione del valore in microsecondi, uno dei valori viene convertito nel tipo di dati **float**.  
  
```  
SELECT @@IO_BUSY*@@TIMETICKS AS 'IO microseconds',   
   GETDATE() AS 'as of';  
```  
  
 Quello che segue è un set di risultati tipico:  
  
```  
  
IO microseconds as of                   
--------------- ----------------------  
4552312500      12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [@@CPU_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funzioni statistiche di sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
