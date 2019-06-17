---
title: sys.service_broker_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_broker_endpoints_TSQL
- service_broker_endpoints
- service_broker_endpoints_TSQL
- sys.service_broker_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_broker_endpoints catalog view
ms.assetid: 6979ec9b-0043-411e-aafb-0226fa26c5ba
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f93ac0b4a11e10d3db952fd850f4c83668a97d3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62855260"
---
# <a name="sysservicebrokerendpoints-transact-sql"></a>sys.service_broker_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa vista del catalogo contiene una riga per l'endpoint di Service Broker. Per ogni riga in questa vista è presente una riga corrispondente con lo stesso **endpoint_id** nel **Sys. tcp_endpoints** vista contenente i metadati di configurazione TCP. TCP è l'unico protocollo consentito in Service Broker.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**\<colonne ereditate >**|**--**|Eredita le colonne da [Sys. Endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_message_forwarding_enabled**|**bit**|Specifica se l'endpoint supporta l'inoltro di messaggi. Viene inizialmente impostato su **0** (disabilitato). Non ammette i valori Null.|  
|**message_forwarding_size**|**int**|Il numero massimo di megabyte di **tempdb** spazi consentiti da utilizzare per l'inoltro di messaggi. Viene inizialmente impostato su **10**. Non ammette i valori Null.|  
|**connection_auth**|**tinyint**|Tipo di autenticazione della connessione necessario per le connessioni all'endpoint. I possibili valori sono i seguenti:<br /><br /> **1** - NTLM<br /><br /> **2** - KERBEROS<br /><br /> **3** - NEGOTIATE<br /><br /> **4** -CERTIFICATO<br /><br /> **5** -NTLM, CERTIFICATO<br /><br /> **6** -KERBEROS, CERTIFICATO<br /><br /> **7** -NEGOTIATE, CERTIFICATI<br /><br /> **8** -CERTIFICATO, NTLM<br /><br /> **9** -CERTIFICATO, KERBEROS<br /><br /> **10** -CERTIFICATO, NEGOTIATE<br /><br /> Non ammette i valori Null.|  
|**connection_auth_desc**|**nvarchar(60)**|Descrizione del tipo di autenticazione della connessione necessario per le connessioni all'endpoint. I possibili valori sono i seguenti:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE<br /><br /> Ammette valori Null.|  
|**certificate_id**|**int**|ID del certificato utilizzato per l'autenticazione, se disponibile.<br /><br /> 0 = viene utilizzata l'autenticazione di Windows.|  
|**encryption_algorithm**|**tinyint**|Algoritmo di crittografia. Di seguito sono i valori possibili con le descrizioni e l'opzione DDL corrispondente.<br /><br /> **0** : NONE. Opzione DDL corrispondente: Disabilitato.<br /><br /> **1** :  RC4. Opzione DDL corrispondente: {necessari &#124; obbligatorio algoritmo RC4}.<br /><br /> **2** : AES. Opzione DDL corrispondente: Algoritmo AES.<br /><br /> **3** : NONE, RC4. Opzione DDL corrispondente: {supportati &#124; supportata algoritmo RC4}.<br /><br /> **4** : NONE, AES. Opzione DDL corrispondente: Algoritmo AES è supportato.<br /><br /> **5** : RC4, AES. Opzione DDL corrispondente: Obbligatorio algoritmo RC4 AES.<br /><br /> **6** : AES, RC4. Opzione DDL corrispondente: Algoritmo AES RC4.<br /><br /> **7** : NONE, RC4, AES. Opzione DDL corrispondente: Supportato algoritmo RC4 AES.<br /><br /> **8** : NONE, AES, RC4. Opzione DDL corrispondente: Algoritmo AES RC4 è supportato.<br /><br /> Non ammette i valori Null.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Descrizione dell'algoritmo di crittografia. I valori possibili e le corrispondenti opzioni di DDL sono elencate di seguito:<br /><br /> NONE: Disabilitata<br /><br /> RC4: {necessari &#124; obbligatorio algoritmo RC4}<br /><br /> AES: Algoritmo AES<br /><br /> NONE, RC4: {supportati &#124; algoritmo RC4 è supportato}<br /><br /> NONE, AES: Algoritmo supportato AES<br /><br /> RC4, AES: Obbligatorio algoritmo RC4 AES<br /><br /> AES, RC4: Algoritmo AES RC4<br /><br /> NONE, RC4, AES: Algoritmo RC4 è supportato AES<br /><br /> NONE, AES, RC4: Algoritmo supportato AES RC4<br /><br /> Ammette valori Null.|  
  
## <a name="remarks"></a>Note  
  
> [!NOTE]  
>  L'algoritmo RC4 è supportato solo per motivi di compatibilità con le versioni precedenti. È possibile crittografare il nuovo materiale usando RC4 o RC4_128 solo quando il livello di compatibilità del database è 90 o 100. (Non consigliato.) Usare un algoritmo più recente, ad esempio uno degli algoritmi AES. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive il materiale crittografato utilizzando RC4 o RC4_128 può essere decrittografato in qualsiasi livello di compatibilità.  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
