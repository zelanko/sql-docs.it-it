---
title: sys.crypt_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- crypt_properties
- crypt_properties_TSQL
- sys.crypt_properties_TSQL
- sys.crypt_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.crypt_properties catalog view
ms.assetid: d5684f5a-30b1-418e-ae4d-ab040db9257e
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8aae950e39dd66bb08a2adbc6225358c75ad4d37
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730164"
---
# <a name="syscryptproperties-transact-sql"></a>sys.crypt_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni proprietà crittografica associata all'entità a protezione diretta.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|Identifica la classe dell'elemento in cui esiste la proprietà.<br /><br /> 1 = Oggetto o colonna<br /> 5 = Assembly|  
|**class_desc**|**nvarchar(60)**|Descrizione della classe dell'elemento in cui esiste la proprietà.<br /><br /> OBJECT_OR_COLUMN<br /> ASSEMBLY|  
|**major_id**|**int**|ID dell'elemento in cui esiste la proprietà, interpretato in base alla classe.|  
|**thumbprint**|**varbinary(32)**|Hash SHA-1 del certificato o chiave asimmetrica utilizzata.|  
|**crypt_type**|**char(4)**|Tipo di crittografia.<br /><br /> SPVC = firmato dalla chiave privata del certificato<br /><br /> SPVA = firmato dalla chiave privata asimmetrica<br /><br /> CPVC = Controfirma tramite la chiave privata del certificato<br /><br /> CPVA = Controfirma tramite la chiave asimmetrica|  
|**crypt_type_desc**|**nvarchar(60)**|Descrizione del tipo di crittografia.<br /><br /> SIGNATURE BY CERTIFICATE<br /><br /> SIGNATURE BY ASYMMETRIC KEY<br /><br /> COUNTER SIGNATURE BY CERTIFICATE<br /><br /> COUNTER SIGNATURE BY ASYMMETRIC KEY|  
|**crypt_property**|**varbinary(max)**|Bit firmati o crittografati. Per un modulo firmato questi sono i bit di firma del modulo.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
