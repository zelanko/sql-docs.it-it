---
title: sys. database_usage (database SQL di Azure) | Microsoft Docs
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0a0789ebd9a5aa4bd10605d69afa59a586ce75b2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155539"
---
# <a name="sysdatabase_usage-azure-sql-database"></a>sys.database_usage (Database di SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Nota: questa opzione si applica solo al database SQL di Azure V11.**  
  
 Elenca il numero, il tipo e la durata dei database nel server [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 La vista **sys. database_usage** contiene le colonne seguenti.  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|time|Data di esecuzione degli eventi di utilizzo.|  
|sku|Tipo di livello di servizio per il database: **Web**, **Business**, **Basic**, **standard**, **Premium**|  
|quantity|Numero massimo di database di un tipo SKU presente durante il giorno.|  
  
## <a name="permissions"></a>Autorizzazioni  
 L'accesso in sola lettura a questa vista è disponibile per tutti gli utenti che dispongono delle autorizzazioni per connettersi al database **Master** .  
  
## <a name="remarks"></a>Osservazioni  
 La vista **sys. database_usage** restituisce una riga per ogni giorno della sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli prezzi del database SQL](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Account e fatturazione nel database SQL di Azure](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
