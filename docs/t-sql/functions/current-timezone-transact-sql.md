---
title: CURRENT_TIMEZONE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURRENT_TIMEZONE
- CURRENT_TIMEZONE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- current time zone [SQL Server]
- current timezone [SQL Server]
- system time zone [SQL Server]
- system timezone [SQL Server]
- functions [SQL Server], time zone
- functions [SQL Server], timezone
- timezone [SQL Server], functions
- time zone [SQL Server], functions
- CURRENT_TIMEZONE function [SQL Server]
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e659ae78b81cb6888e749bd40546efe16b4c542d
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2019
ms.locfileid: "72261333"
---
# <a name="current_timezone-transact-sql"></a>CURRENT_TIMEZONE (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Questa funzione restituisce il nome del fuso orario osservato da un server o un'istanza. Per Istanza gestita di database SQL, il valore restituito è basato sul fuso orario dell'istanza stessa assegnato durante la creazione dell'istanza e non sul fuso orario del sistema operativo sottostante.
  
> [!NOTE]  
> Per i database SQL singolo e in pool il fuso orario è sempre impostato su UTC e `CURRENT_TIMEZONE` restituisce il nome del fuso orario UTC.
  
## <a name="syntax"></a>Sintassi  
  
```sql
CURRENT_TIMEZONE ( )  
```
  
## <a name="arguments"></a>Argomenti

Questa funzione non accetta argomenti
  
## <a name="return-type"></a>Tipo restituito  

**varchar**
  
## <a name="remarks"></a>Remarks  

`CURRENT_TIMEZONE` è una funzione non deterministica. Le viste e le espressioni in cui viene fatto riferimento a questa colonna non sono indicizzabili.
  
## <a name="example"></a>Esempio

Si noti che il valore restituito riflette il fuso orario effettivo e le impostazioni della lingua del server o dell'istanza.

```sql
SELECT CURRENT_TIMEZONE();  
/* Returned:  
(UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna 
*/
```  
  
## <a name="see-also"></a>Vedere anche

[Fuso orario dell'istanza gestita di database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-timezone)
