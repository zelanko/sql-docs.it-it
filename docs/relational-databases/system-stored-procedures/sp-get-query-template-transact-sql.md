---
title: sp_get_query_template (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_get_query_template
- sp_get_query_template_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_query_template
ms.assetid: 85e9bef7-2417-41a8-befa-fe75507d9bf2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9841e7815f31af26aeeb3ed0f4783d3a36d83030
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124078"
---
# <a name="spgetquerytemplate-transact-sql"></a>sp_get_query_template (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce il formato con parametri di una query. I risultati restituiti sono simili al formato con parametri di una query risultante dall'utilizzo della parametrizzazione forzata. sp_get_query_template viene principalmente utilizzata durante la creazione delle guide di piano TEMPLATE.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_get_query_template  
   [ @querytext = ] N'query_text'  
   , @templatetext OUTPUT   
   , @parameters OUTPUT   
```  
  
## <a name="arguments"></a>Argomenti  
 «*query_text*»  
 Query per la quale la versione con parametri deve essere generata. «*query_text*' deve essere racchiuso tra virgolette singole ed essere preceduto dall'identificatore Unicode N. N'*query_text*' è il valore assegnato per il @querytext parametro. Il tipo è **nvarchar (max)** .  
  
 @templatetext  
 È un parametro di output di tipo **nvarchar (max)** , specificato come indicato, che riceve la forma parametrizzata della *query_text* come valore letterale stringa.  
  
 @parameters  
 È un parametro di output di tipo **nvarchar (max)** , specificato come indicato, che riceve un valore letterale stringa dei dati e i nomi dei tipi di parametro che sono stati associati parametri in @templatetext.  
  
## <a name="remarks"></a>Note  
 sp_get_query_template restituisce un errore se:  
  
-   Non assegna parametri in valori letterali costanti *query_text*.  
  
-   *query_text* è NULL, non una stringa Unicode, non è sintatticamente valida o non può essere compilato.  
  
 Se sp_get_query_template restituisce un errore, non modifica i valori del @templatetext e @parameters i parametri di output.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo del database public.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il formato con parametri di una query contenente due valori letterali costanti.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @my_templatetext nvarchar(max)  
DECLARE @my_parameters nvarchar(max)  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
        FROM Production.ProductModel pm   
        INNER JOIN Production.ProductInventory pi  
        ON pm.ProductModelID = pi.ProductID  
        WHERE pi.ProductID = 2  
        GROUP BY pi.ProductID, pi.Quantity  
        HAVING SUM(pi.Quantity) > 400',  
@my_templatetext OUTPUT,  
@my_parameters OUTPUT;  
SELECT @my_templatetext;  
SELECT @my_parameters;  
```  
  
 Di seguito sono riportati i risultati con parametri del parametro `@my_templatetext``OUTPUT`.  
  
 `select pi . ProductID , SUM ( pi . Quantity ) as Total`  
  
 `from Production . ProductModel pm`  
  
 `inner join Production . ProductInventory pi`  
  
 `on pm . ProductModelID = pi . ProductID`  
  
 `where pi . ProductID = @0`  
  
 `group by pi . ProductID , pi . Quantity`  
  
 `having SUM ( pi . Quantity ) > 400`  
  
 Il primo valore letterale costante, `2`, viene convertito in parametro. Il secondo valore letterale, `400`, non viene convertito perché si trova all'interno di una clausola `HAVING`. I risultati restituiti da sp_get_query_template sono simili al formato con parametri di una query se l'opzione PARAMETERIZATION dell'istruzione ALTER DATABASE è impostata su FORCED.  
  
 Di seguito sono riportati i risultati con parametri del parametro `@my_parameters OUTPUT`.  
  
```  
@0 int  
```  
  
> [!NOTE]  
>  L'ordine e la denominazione dei parametri nell'output della stored procedure sp_get_query_template possono variare tra correzioni QFE (Quick Fix Engineering), Service Pack e aggiornamenti di versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È inoltre possibile che in seguito agli aggiornamenti vengano assegnati parametri a un set di valori letterali costanti diverso per la stessa query e che una spaziatura diversa venga applicata ai risultati in entrambi i parametri di output.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Specificare il comportamento di parametrizzazione delle query tramite guide di piano](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)  
  
  
