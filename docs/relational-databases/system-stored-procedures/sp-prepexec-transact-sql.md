---
title: sp_prepexec (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexec
- sp_cursor_prepexec_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexec
ms.assetid: f9141850-a62b-43bf-8e46-b2f92b75ca56
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3bc3e9a74a29564ad8c531223be371f47fd09662
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891536"
---
# <a name="sp_prepexec-transact-sql"></a>sp_prepexec (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Prepara ed esegue un'istruzione con parametri [!INCLUDE[tsql](../../includes/tsql-md.md)] . sp_prepexec combina le funzioni di sp_prepare e sp_execute. Questa azione viene richiamata da ID = 13 in un pacchetto TDS (Tabular Data Stream).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_prepexec handle OUTPUT, params , stmt  
    [ , bound param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *gestire*  
 Identificatore dell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *handle* generato da. *handle* è un parametro obbligatorio con un valore restituito **int** .  
  
 *params*  
 Identifica le istruzioni con parametri. La definizione *params* delle variabili viene sostituita per i marcatori di parametro nell'istruzione. *params* è un parametro obbligatorio che richiede un valore di input **ntext**, **nchar**o **nvarchar** . Immettere un valore NULL se l'istruzione non è con parametri.  
  
 *stmt*  
 Definisce il set di risultati del cursore. Il parametro *stmt* è obbligatorio e richiede un valore di input **ntext**, **nchar**o **nvarchar** .  
  
 *bound_param*  
 Indica l'utilizzo facoltativo di parametri aggiuntivi. *bound_param* chiama un valore di input di qualsiasi tipo di dati per definire i parametri aggiuntivi in uso.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene preparata ed eseguita un'istruzione semplice:  
  
```  
Declare @Out int;  
EXEC sp_prepexec @Out output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name  
      FROM sys.databases  
      WHERE name=@P1 AND state_desc = @P2',   
          @P1 = 'tempdb', @P2 = 'ONLINE';   
EXEC sp_unprepare @Out;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_execute &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-execute-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
