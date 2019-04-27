---
title: xp_sqlmaint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2157462ca1f9509034f33208cce7aed2983ae4f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62644799"
---
# <a name="xpsqlmaint-transact-sql"></a>xp_sqlmaint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Chiama il **sqlmaint** utilità con una stringa che contiene **sqlmaint**commutatori. Il **sqlmaint** utilità esegue una serie di operazioni di manutenzione su uno o più database.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>Argomenti  
 **'** *switch_string* **'**  
 È una stringa contenente il **sqlmaint** opzioni dell'utilità. Le opzioni e i relativi valori devono essere separati da uno spazio.  
  
 Il **-?** non è valida per **xp_sqlmaint**.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Nessuna. Restituisce un errore se il **sqlmaint** utilità ha esito negativo.  
  
## <a name="remarks"></a>Note  
 Se questa procedura viene chiamata da un utente l'accesso con autenticazione di SQL Server, il **- U "***login_id***"** e **-P "***password***"** commutatori vengono aggiunti all'inizio *switch_string* prima dell'esecuzione. Se l'utente è connesso con l'autenticazione di Windows *switch_string* viene passato senza apportare modifiche **sqlmaint**.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente `xp_sqlmaint` viene chiamata da `sqlmaint` per eseguire controlli di integrità, creare un file di report e aggiornare `msdb.dbo.sysdbmaintplan_history`.  
  
```  
EXEC xp_sqlmaint '-D AdventureWorks2012 -PlanID 02A52657-D546-11D1-9D8A-00A0C9054212   
   -Rpt "C:\Program Files\Microsoft SQL Server\MSSQL\LOG\DBMaintPlan2.txt" -WriteHistory  -CkDB -CkAl';   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The command(s) executed successfully.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità sqlmaint](../../tools/sqlmaint-utility.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
