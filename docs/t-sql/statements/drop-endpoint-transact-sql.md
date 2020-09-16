---
description: DROP ENDPOINT (Transact-SQL)
title: DROP ENDPOINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_ENDPOINT_TSQL
- DROP ENDPOINT
dev_langs:
- TSQL
helpviewer_keywords:
- removing endpoints
- endpoints [SQL Server], removing
- deleting endpoints
- DROP ENDPOINT statement
- dropping endpoints
ms.assetid: 6aca7412-66a5-4fa4-86b2-061512ff2080
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a33cf6c43f2f01e3a897a0491954b98e5739db6e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539828"
---
# <a name="drop-endpoint-transact-sql"></a>DROP ENDPOINT (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Elimina un endpoint esistente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP ENDPOINT endPointName  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *endPointName*  
 Nome dell'endpoint da rimuovere.  
  
## <a name="remarks"></a>Osservazioni  
 Non è possibile eseguire le istruzioni ENDPOINT DDL all'interno di una transazione utente.  
  
## <a name="permissions"></a>Autorizzazioni  
 L'utente deve essere membro del ruolo predefinito del server **sysadmin**, proprietario dell'endpoint oppure disporre dell'autorizzazione CONTROL per l'endpoint.  
  
## <a name="examples"></a>Esempio  
 Nell'esempio seguente viene rimosso l'endpoint denominato `sql_endpoint` precedentemente creato.  
  
```  
DROP ENDPOINT sql_endpoint;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
