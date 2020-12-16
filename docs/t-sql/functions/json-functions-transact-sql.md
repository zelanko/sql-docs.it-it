---
description: Funzioni JSON (Transact-SQL)
title: Funzioni JSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
helpviewer_keywords:
- JSON functions
ms.assetid: ec97d451-06af-44a3-8304-305d410cfc8e
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017
ms.openlocfilehash: c55ffdeec513c71c89cd5ed4bb8ef9f6e88e7330
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478612"
---
# <a name="json-functions-transact-sql"></a>Funzioni JSON (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

Usare le funzioni descritte nelle pagine di questa sezione per convalidare o modificare testo JSON oppure per estrarre valori semplici o complessi.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[ISJSON](../../t-sql/functions/isjson-transact-sql.md)|Verifica se una stringa include contenuto JSON valido.|  
|[JSON_VALUE](../../t-sql/functions/json-value-transact-sql.md)|Estrae un valore scalare da una stringa JSON.|  
|[JSON_QUERY](../../t-sql/functions/json-query-transact-sql.md)|Estrae un oggetto o una matrice da una stringa JSON.|  
|[JSON_MODIFY](../../t-sql/functions/json-modify-transact-sql.md)|Aggiorna il valore di una proprietà in una stringa JSON e restituisce la stringa JSON aggiornata.|

 Per altre informazioni sul supporto integrato per JSON in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Dati JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md).  

## <a name="see-also"></a>Vedi anche

 - [Convalidare, eseguire query e modificare i dati JSON con funzioni predefinite &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)
 - [JSON Path Expressions (Espressioni di percorso JSON) &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)
 - [Dati JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
