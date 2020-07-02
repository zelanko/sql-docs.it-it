---
title: sp_testlinkedserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_testlinkedserver
- sp_testlinkedserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_testlinkedserver
ms.assetid: e63ca7d4-47d6-455e-9aac-421f9683dadc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 27fd5a01211fabd1399fe45f2c30b043368d5f0a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750410"
---
# <a name="sp_testlinkedserver-transact-sql"></a>sp_testlinkedserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Consente di testare la connessione a un server collegato. Se il test ha esito negativo, tramite la procedura viene generata un'eccezione con il motivo dell'errore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_testlinkedserver [ @servername ] = servername  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @servername = ]servername`Nome del server collegato. *nomeserver* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="permissions"></a>Autorizzazioni  
 Le autorizzazioni non vengono controllate, tuttavia il chiamante deve disporre del mapping di account di accesso appropriato.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creato un server collegato denominato `SEATTLESales` e viene quindi testata la connessione.  
  
```  
USE master;  
GO  
EXEC sp_addlinkedserver   
    'SEATTLESales',  
    N'SQL Server';  
GO  
sp_testlinkedserver SEATTLESales;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addlinkedserver &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)  
  
  
