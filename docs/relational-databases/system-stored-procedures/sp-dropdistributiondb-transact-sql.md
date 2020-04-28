---
title: sp_dropdistributiondb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistributiondb_TSQL
- sp_dropdistributiondb
helpviewer_keywords:
- sp_dropdistributiondb
ms.assetid: b6dd1846-2259-4d29-93af-a70a5d25a0c5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 960da4d98ea33ceb3ecdb48e36d565854484feb9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68768865"
---
# <a name="sp_dropdistributiondb-transact-sql"></a>sp_dropdistributiondb (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Elimina un database di distribuzione. Rimuove i file fisici utilizzati dal database se non sono utilizzati da un altro database. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropdistributiondb [ @database= ] 'database'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @database = ] 'database'`Database da eliminare. il *database* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_dropdistributiondb** viene utilizzato in tutti i tipi di replica.  
  
 È necessario eseguire questa stored procedure prima di eliminare il server di distribuzione eseguendo **sp_dropdistributor**.  
  
 **sp_dropdistributiondb** rimuove anche un processo di agente di lettura coda per il database di distribuzione, se disponibile.  
  
 Per disabilitare la distribuzione, è necessario che il database di distribuzione sia online. Se esiste uno snapshot per il database di distribuzione, deve essere eliminato prima della disabilitazione della distribuzione. Uno snapshot del database è una copia offline e di sola lettura di un database e non è correlato a uno snapshot di replica. Per altre informazioni, vedere [Snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributiondb-tr_1.sql)]  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_dropdistributiondb**.  
  
## <a name="see-also"></a>Vedere anche  
 [Disabilitare la pubblicazione e la distribuzione](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistributiondb &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
