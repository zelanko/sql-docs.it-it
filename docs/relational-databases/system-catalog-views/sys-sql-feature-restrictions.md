---
title: sys.sql_feature_restrictions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/07/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_sql_feature_restrictions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_feature_restrictions catalog view
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b583afef9f52da7801384d4a7a9c76deaf8d4ee4
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822681"
---
# <a name="syssqlfeaturerestrictions-transact-sql"></a>sys.sql_feature_restrictions (Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Restituisce una riga per ogni restrizione nel database.
  
| Nome colonna | Tipo di dati | Descrizione |
|-------------|-----------|-------------|
| class       | nvarchar(128) | Classe dell'oggetto a cui viene applicata la restrizione |
| oggetto      | nvarchar(256) | Nome dell'oggetto a cui viene applicata la restrizione |
| Funzionalità     | nvarchar(128) | Funzionalità limitata |
  
## <a name="remarks"></a>Note

Attualmente le seguenti funzionalità può essere limitata:

| Funzionalità          | Descrizione |
|------------------|-------------|
| N'ErrorMessages' | Quando la limitata, verranno applicata la maschera dati utente all'interno del messaggio di errore. |
| N'Waitfor'       | Quando la limitata, il comando restituirà immediatamente senza alcun ritardo. |
  
## <a name="permissions"></a>Permissions

Entità di esecuzione deve avere il `CONTROL` autorizzazione per il database.
  
## <a name="see-also"></a>Vedere anche

 [Limitazioni delle funzionalità](../../relational-databases/security/feature-restrictions.md)
