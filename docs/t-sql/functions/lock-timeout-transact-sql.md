---
title: '@@LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@LOCK_TIMEOUT'
- '@@LOCK_TIMEOUT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- '@@LOCK_TIMEOUT function'
- current lock time-out setting
- locking [SQL Server], time-outs
ms.assetid: 6bf8bf97-60b8-40c1-b89d-8f5a00bcae2e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 767ccc61139886a1e81bbeb390b89676267b0d79
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68059897"
---
# <a name="x40x40lock_timeout-transact-sql"></a>&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce l'impostazione corrente del timeout del blocco, in millisecondi, per la sessione corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **integer**  
  
## <a name="remarks"></a>Osservazioni  
 L'istruzione SET LOCK_TIMEOUT consente a un'applicazione di impostare il periodo di tempo massimo durante il quale un'istruzione rimane in attesa di una risorsa bloccata. Quando il periodo di attesa di un'istruzione supera il valore massimo impostato con l'opzione LOCK_TIMEOUT, l'istruzione bloccata viene annullata automaticamente e nell'applicazione viene restituito un messaggio di errore.  
  
 @@LOCK_TIMEOUT restituisce il valore -1 se l'istruzione SET LOCK_TIMEOUT non è stata ancora eseguita nella sessione corrente.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato il set di risultati ottenuto quando per l'opzione LOCK_TIMEOUT non è stato impostato alcun valore.  
  
```  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 Set di risultati:  
  
```  
Lock Timeout  
------------  
-1  
```  
  
 Nell'esempio seguente l'opzione LOCK_TIMEOUT viene impostata su 1800 millisecondi, quindi viene richiamata la funzione @@LOCK_TIMEOUT.  
  
```  
SET LOCK_TIMEOUT 1800;  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 Set di risultati:  
  
```  
Lock Timeout  
------------  
1800          
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di configurazione &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
