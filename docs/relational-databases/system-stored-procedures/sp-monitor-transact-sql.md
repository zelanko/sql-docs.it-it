---
title: sp_monitor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_monitor_TSQL
- sp_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_monitor
ms.assetid: cb628496-2f9b-40e4-b018-d0831c4cb018
author: stevestein
ms.author: sstein
ms.openlocfilehash: d91f774973588096ea73675d9b0e9ebf6368f1ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68022322"
---
# <a name="sp_monitor-transact-sql"></a>sp_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza le statistiche [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]relative a.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**last_run**|Ora dell'ultima esecuzione **sp_monitor** .|  
|**current_run**|Tempo di esecuzione **sp_monitor** .|  
|**secondi**|Numero di secondi trascorsi dall'esecuzione **sp_monitor** .|  
|**cpu_busy**|Numero di secondi di attività della CPU del server per l'elaborazione di operazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**io_busy**|Numero di secondi trascorsi per l'esecuzione di operazioni di input e output in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**inattivo**|Numero di secondi durante i quali [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è rimasto inattivo.|  
|**packets_received**|Numero di pacchetti di input letti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**packets_sent**|Numero di pacchetti di output scritti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**packet_errors**|Numero di errori rilevati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante la lettura e la scrittura di pacchetti.|  
|**total_read**|Numero di letture eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**total_write**|Numero di scritture eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**total_errors**|Numero di errori rilevati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante la lettura e la scrittura.|  
|**connessioni**|Numero di accessi o tentativi di accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="remarks"></a>Osservazioni  
 Tramite una serie di funzioni, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene tenuto traccia della quantità di operazioni eseguite. L'esecuzione di **sp_monitor** Visualizza i valori correnti restituiti da queste funzioni e Mostra la quantità di modifiche apportate dall'ultima esecuzione della stored procedure.  
  
 Per ogni colonna, la statistica viene stampata nel formato *numero*(*numero*):*numero*% o *numero*(*numero*). Il primo *numero* indica il numero di secondi (per **CPU_BUSY**, **IO_BUSY**e **Idle**) oppure il numero totale (per le altre variabili) dopo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il riavvio di. Il *numero* tra parentesi si riferisce al numero di secondi o al numero totale dall'ultima volta in cui è stato eseguito **sp_monitor** . La percentuale è la percentuale di tempo trascorso dall'ultima esecuzione **sp_monitor** . Se, ad esempio, il report Mostra **CPU_BUSY** come 4250 (215)-68%, la CPU è stata occupata 4250 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] secondi dall'ultimo avvio, 215 secondi dall'ultima esecuzione di **sp_monitor** e 68% del tempo totale trascorso dall'ultima esecuzione di **sp_monitor** .  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni relative all'attività di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
||||  
|-|-|-|  
|**last_run**|**current_run**|**secondi**|  
|1998-03-29 11.55|1998-04-04 14.22|561|  
  
||||  
|-|-|-|  
|**cpu_busy**|**io_busy**|**inattivo**|  
|190 (0)-0%|187 (0)-0%|148 (556)-99%|  
  
||||  
|-|-|-|  
|**packets_received**|**packets_sent**|**packet_errors**|  
|16 (1)|20 (2)|0 (0)|  
  
|||||  
|-|-|-|-|  
|**total_read**|**total_write**|**total_errors**|**connessioni**|  
|141 (0)|54920 (127)|0 (0)|4 (0)|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_who &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
