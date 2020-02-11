---
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: ff099e48540b7255e2453bfb9b90c9515196449c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68005092"
---
# <a name="sysdm_cryptographic_provider_sessions-transact-sql"></a>sys.dm_cryptographic_provider_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
|**identità**|**nvarchar(128)**|Identità utilizzata per l'autenticazione con il provider di crittografia.|  
|**spid**|**short**|ID sessione (SPID) della connessione. Per altre informazioni, vedere [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md).|  
  
## <a name="remarks"></a>Osservazioni  
 La vista **sys. dm_cryptographic_provider_sessions** è visibile al pubblico per la connessione corrente. Per visualizzare tutte le connessioni crittografiche, è necessario disporre dell'autorizzazione **Control** server.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
