---
title: dbo. server_quotas (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 657376be08e4cd404ce53d78114604cdd11fbda2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63005837"
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas (Database di SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **IMPORTANTE** Si applica a  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 solo!**  
>   
>  Questa funzionalità si trova nello stato anteprima. Non specificare una dipendenza dall'implementazione specifica di questa funzionalità perché potrebbe essere modificata o rimossa in una versione successiva.  
  
 Restituisce i tipi di quote di database disponibili nel server.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|Tipo di quota per il server. Il tipo **Premium_database** equivale ai database con una prenotazione delle risorse.|  
|quota_value|**int**|Numero di tipo di quota consentito nel server.|  
  
## <a name="permissions"></a>Permissions  
 Questa vista è disponibile per tutti i ruoli utente con autorizzazioni sufficienti per connettersi a virtual **master** database.  
  
## <a name="see-also"></a>Vedere anche  
 [La gestione di database Premium](https://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
