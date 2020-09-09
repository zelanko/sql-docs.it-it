---
description: sys.dm_cryptographic_provider_sessions (Transact-SQL)
title: sys. dm_cryptographic_provider_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cryptographic_provider_sessions
- dm_cryptographic_provider_sessions_TSQL
- sys.dm_cryptographic_provider_sessions_TSQL
- dm_cryptographic_provider_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_sessions dynamic management function
ms.assetid: 9a4de02b-1a07-4850-979a-0861fddb7f9d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 223d3b1ebac4230436f069c2ec9415e7d57feb3f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542290"
---
# <a name="sysdm_cryptographic_provider_sessions-transact-sql"></a>sys.dm_cryptographic_provider_sessions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce informazioni sulle sessioni aperte per un provider di crittografia.  
 
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.dm_cryptographic_provider_sessions(session_identifier)  
```  
  
## <a name="arguments"></a>Argomenti  
 *session_identifier*  
 Un numero intero che indica le sessioni da restituire.  
  
 0 = solo connessione corrente  
  
 1 = tutte le connessioni di crittografia  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|Numero di identificazione del provider di crittografia.|  
|**session_handle**|**varbytes (8)**|Handle della sessione di crittografia.|  
|**identity**|**nvarchar(128)**|Identità utilizzata per l'autenticazione con il provider di crittografia.|  
|**spid**|**short**|ID sessione (SPID) della connessione. Per altre informazioni, vedere [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md).|  
  
## <a name="remarks"></a>Osservazioni  
 La vista **sys. dm_cryptographic_provider_sessions** è visibile al pubblico per la connessione corrente. Per visualizzare tutte le connessioni crittografiche, è necessario disporre dell'autorizzazione **Control** server.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
