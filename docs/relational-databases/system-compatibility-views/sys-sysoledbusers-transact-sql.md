---
title: sys. sysoledbusers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysoledbusers
- sys.sysoledbusers_TSQL
- sysoledbusers
- sysoledbusers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoledbusers system table
- sys.sysoledbusers compatibility view
ms.assetid: fe924c17-9cad-4b2b-8124-1e0fd82931e3
author: rothja
ms.author: jroth
ms.openlocfilehash: d7c8b97a04e8b9898a9d49a412c5c6e5a2aa910c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076529"
---
# <a name="syssysoledbusers-transact-sql"></a>sys.sysoledbusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  Questa tabella di sistema di [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] è disponibile come vista in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per motivi di compatibilità con le versioni precedenti. È consigliabile utilizzare invece le [viste del catalogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) .  
  
 È contenuta una riga per il mapping di ogni utente e password per il server collegato specificato. **sysoledbusers** è archiviato nel database **Master** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**rmtsrvid**|**smallint**|ID di sicurezza (SID) del server.|  
|**rmtloginame**|**nvarchar (** 128 **)**|Nome dell'account di accesso remoto a cui **LoginSid** esegue il mapping per **rmtservid**collegati.|  
|**rmtpassword**|**nvarchar (** 128 **)**|Restituisce NULL.|  
|**LoginSid**|**varbinary (** 85 **)**|SID dell'account di accesso locale su cui eseguire il mapping.|  
|**stato**|**smallint**|Se uguale a 1, per il mapping è necessario utilizzare le credenziali dell'utente.|  
|**changedate**|**datetime**|Data dell'ultima modifica delle informazioni sul mapping.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Viste di compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
