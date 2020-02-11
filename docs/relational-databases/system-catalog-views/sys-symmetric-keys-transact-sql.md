---
title: sys. symmetric_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- symmetric_keys
- sys.symmetric_keys
- sys.symmetric_keys_TSQL
- symmetric_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.symmetric_keys catalog view
ms.assetid: d410eae1-3a52-45de-b9a1-52d2bd93a8eb
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5b4607c5873889c17e9934cc4f24465fe4e83007
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68108935"
---
# <a name="syssymmetric_keys-transact-sql"></a>sys.symmetric_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una riga per ogni chiave simmetrica creata con l'istruzione CREATE SYMMETRIC KEY.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome della chiave. Univoco all'interno del database.|  
|**principal_id**|**int**|ID dell'entità di database proprietaria della sottoscrizione.|  
|**symmetric_key_id**|**int**|ID della chiave. Univoco all'interno del database.|  
|**key_length**|**int**|Lunghezza della chiave in bit.|  
|**key_algorithm**|**carattere (2)**|Algoritmo utilizzato con la chiave:<br /><br /> R2 = RC2<br /><br /> R4 = RC4<br /><br /> D = DES<br /><br /> D3 = Triple DES<br /><br /> DT = TRIPLE_DES_3KEY<br /><br /> DX = DESX<br /><br /> A1 = AES 128<br /><br /> A2 = AES 192<br /><br /> A3 = AES 256<br /><br /> NA = Chiave EKM|  
|**algorithm_desc**|**nvarchar (60)**|Descrizione dell'algoritmo utilizzato con la chiave.<br /><br /> RC2<br /><br /> RC4<br /><br /> DES<br /><br /> Triple_DES<br /><br /> TRIPLE_DES_3KEY<br /><br /> DESX<br /><br /> AES_128<br /><br /> AES_192<br /><br /> AES_256<br /><br /> NULL (solo algoritmi EKM)|  
|**create_date**|**datetime**|Data di creazione della chiave.|  
|**modify_date**|**datetime**|Data di modifica della chiave.|  
|**key_guid**|**uniqueidentifier**|Identificatore univoco globale (GUID) associato alla chiave. Generato automaticamente per le chiavi persistenti. I GUID per le chiavi temporanee derivano dalla passphrase specificata dall'utente.|  
|**key_thumbprint**|**sql_variant**|Hash SHA-1 della chiave. L'hash è univoco a livello globale. Per le chiavi non EKM questo valore è NULL.|  
|**provider_type**|**nvarchar (120)**|Tipo di provider del servizio di crittografia:<br /><br /> CRYPTOGRAPHIC PROVIDER = chiavi EKM<br /><br /> NULL = chiavi non EKM|  
|**cryptographic_provider_guid**|**uniqueidentifier**|GUID del provider del servizio di crittografia. Per le chiavi non EKM questo valore è NULL.|  
|**cryptographic_provider_algid**|**sql_variant**|ID dell'algoritmo del provider del servizio di crittografia. Per le chiavi non EKM questo valore è NULL.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]Per altre informazioni, vedere [configurazione della visibilità dei metadati](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Osservazioni  
 L'algoritmo RC4 è deprecato. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
> [!NOTE]  
>  L'algoritmo RC4 è supportato solo per motivi di compatibilità con le versioni precedenti. È possibile crittografare il nuovo materiale usando RC4 o RC4_128 solo quando il livello di compatibilità del database è 90 o 100. (Non consigliato.) Usare un algoritmo più recente, ad esempio uno degli algoritmi AES. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] il materiale crittografato utilizzando RC4 o RC4_128 può essere decrittografato in qualsiasi livello di compatibilità.  
  
 **Chiarimento relativo agli algoritmi DES:**  
  
-   La crittografia DESX è stata menzionata erroneamente. Le chiavi simmetriche create con ALGORITHM = DESX utilizzano in realtà la crittografia TRIPLE DES con una chiave a 192 bit. L'algoritmo DESX non è disponibile. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
-   Le chiavi simmetriche create con ALGORITHM = TRIPLE_DES_3KEY utilizzano TRIPLE DES con una chiave a 192 bit.  
  
-   Le chiavi simmetriche create con ALGORITHM = TRIPLE_DES utilizzano TRIPLE DES con una chiave a 128 bit.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Viste del catalogo di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
