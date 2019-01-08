---
title: Sys. database_mirroring_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_endpoints_TSQL
- database_mirroring_endpoints
- sys.database_mirroring_endpoints
- database_mirroring_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HADR [SQL Server], endpoint
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_endpoints catalog view
ms.assetid: f2285199-97ad-473c-a52d-270044dd862b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0aa757203ba82794a0564e50c715134e502c6ac1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538067"
---
# <a name="sysdatabasemirroringendpoints-transact-sql"></a>sys.database_mirroring_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per l'endpoint del mirroring del database di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Endpoint di mirroring del database supporta entrambe le sessioni tra i partner di mirroring del database e con i server di controllo e le sessioni tra la replica primaria di un gruppo di disponibilità Always On e delle relative repliche secondarie.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**\<colonne ereditate >**|-|Eredita le colonne da **Sys. Endpoints** (per altre informazioni, vedere [Sys. Endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)).|  
|**Ruolo**|**tinyint**|Ruolo del mirroring. I possibili valori sono i seguenti:<br /><br /> **0** = nessuno<br /><br /> **1** = partner<br /><br /> **2** = server di controllo<br /><br /> **3** = all<br /><br /> Nota: Questo valore è rilevante solo per il mirroring del database.|  
|**role_desc**|**nvarchar(60)**|Descrizione del ruolo del mirroring. I possibili valori sono i seguenti:<br /><br /> **NONE**<br /><br /> **PARTNER**<br /><br /> **CONTROLLO DEL MIRRORING**<br /><br /> **ALL**<br /><br /> Nota: Questo valore è rilevante solo per il mirroring del database.|  
|**is_encryption_enabled**|**bit**|**1** significa che la crittografia è abilitata.<br /><br /> **0** significa che la crittografia è disabilitata.|  
|**connection_auth**|**tinyint**|Tipo di autenticazione della connessione necessario per le connessioni all'endpoint. I possibili valori sono i seguenti:<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -NEGOTIATE<br /><br /> **4** -CERTIFICATO<br /><br /> **5** -NTLM, CERTIFICATO<br /><br /> **6** -KERBEROS, CERTIFICATO<br /><br /> **7** -NEGOTIATE, CERTIFICATI<br /><br /> **8** -CERTIFICATO, NTLM<br /><br /> **9** -CERTIFICATO, KERBEROS<br /><br /> **10** -CERTIFICATO, NEGOTIATE|  
|**connection_auth_desc**|**Nvarchar (60)**|Descrizione del tipo di autenticazione necessario per le connessioni all'endpoint. I possibili valori sono i seguenti:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE|  
|**certificate_id**|**int**|ID del certificato utilizzato per l'autenticazione, se disponibile.<br /><br /> 0 = viene utilizzata l'autenticazione di Windows.|  
|**encryption_algorithm**|**tinyint**|Algoritmo di crittografia. I valori possibili sono i seguenti:<br /><br /> **0** -NESSUNO<br /><br /> **1** -RC4<br /><br /> **2** -AES<br /><br /> **3** -NONE, RC4<br /><br /> **4** -NESSUNO, AES<br /><br /> **5** -RC4, AES<br /><br /> **6** -AES, RC4<br /><br /> **7** -NONE, RC4, AES<br /><br /> **8** -NESSUNO, AES, RC4|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Descrizione dell'algoritmo di crittografia. I valori possibili sono i seguenti:<br /><br /> Nessuno<br /><br /> RC4<br /><br /> AES<br /><br /> NONE, RC4<br /><br /> NONE, AES<br /><br /> RC4, AES<br /><br /> AES, RC4<br /><br /> NONE, RC4, AES<br /><br /> NONE, AES, RC4|  
  
## <a name="remarks"></a>Note  
  
> [!NOTE]  
>  L'algoritmo RC4 è supportato solo per motivi di compatibilità con le versioni precedenti. È possibile crittografare il nuovo materiale usando RC4 o RC4_128 solo quando il livello di compatibilità del database è 90 o 100. (Non consigliato.) Usare un algoritmo più recente, ad esempio uno degli algoritmi AES. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive il materiale crittografato utilizzando RC4 o RC4_128 può essere decrittografato in qualsiasi livello di compatibilità.  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Specificare l'URL dell'Endpoint quando si aggiunge o modifica una Replica di disponibilità &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)   
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [Endpoint del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Domande frequenti sull'esecuzione di query nel catalogo di sistema di SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
