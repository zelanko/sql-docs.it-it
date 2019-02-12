---
title: Sys. database_usage (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- database_usage
- database_usage_TSQL
- sys.database_usage_TSQL
- sys.database_usage
dev_langs:
- TSQL
helpviewer_keywords:
- database_usage
- sys.database_usage
ms.assetid: be6820de-60bf-4ddd-ace7-4077893d630f
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 62942e939c1221b90b623db12c922f3dcc580c99
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024902"
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Database di SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Nota: Si applica solo al Database di SQL Azure V11.**  
  
 Elenca il numero, tipo e durata dei database sul [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server.  
  
 Il **Sys. database_usage** vista contiene le colonne seguenti.  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|time|Data di esecuzione degli eventi di utilizzo.|  
|sku|Tipo del livello del servizio del database: **Web**, **Business**, **Basic**, **Standard**, **Premium**|  
|quantity|Numero massimo di database di un tipo SKU presente durante il giorno.|  
  
## <a name="permissions"></a>Permissions  
 Accesso in lettura a questa vista è disponibile per tutti gli utenti con autorizzazioni sufficienti per connettersi al **master** database.  
  
## <a name="remarks"></a>Note  
 Il **Sys. database_usage** vista restituisce una riga per ogni giorno della sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli prezzi del Database SQL](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Account e fatturazione nel Database SQL di Azure](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
