---
title: Opzione di configurazione del server column encryption enclave type | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: jroth
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 1031bdfa3aa6c728d3e33b500fe942d5e52c5fdc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799465"
---
# <a name="column-encryption-enclave-type-server-configuration-option"></a>Opzione di configurazione del server column encryption enclave type
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  Usarel'opzione **column encryption enclave type** per abilitare o disabilitare un enclave sicuro per Always Encrypted.  Per altre informazioni, vedere [Always Encrypted con enclave sicuri](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

 La tabella seguente elenca i valori possibili di **column encryption enclave type**:  
  
|valore|Descrizione|  
|-------------------|-----------------|  
|0|**No secure enclave** (Nessun enclave sicuro). [!INCLUDE[ssDE](../../includes/ssde-md.md)] non inizializza l'enclave sicuro per Always Encrypted. Di conseguenza non è disponibile la funzionalità Always Encrypted con enclave sicuri.|  
|1|**Sicurezza basata sulla virtualizzazione (VBS)** . [!INCLUDE[ssDE](../../includes/ssde-md.md)] inizializza l'enclave sicuro (un enclave di memoria sicuro VBS) per Always Encrypted.|    

> [!IMPORTANT]
> Le modifiche a **column encryption enclave type** non hanno effetto finché non si riavvia l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
   
## <a name="examples"></a>Esempi  
 L'esempio seguente abilita l'enclave sicuro:  

```sql  
sp_configure 'column encryption enclave type', 1;  
GO  
RECONFIGURE;  
GO  
```  

L'esempio seguente disabilita l'enclave sicuro:  

```sql  
sp_configure 'column encryption enclave type', 0;  
GO  
RECONFIGURE;  
GO  
```  

## <a name="see-also"></a>Vedere anche  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
