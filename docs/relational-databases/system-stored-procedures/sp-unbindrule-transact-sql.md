---
title: sp_unbindrule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unbindrule_TSQL
- sp_unbindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindrule
ms.assetid: f54ee155-c3c9-4f1a-952e-632a8339f0cc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 86efa9f7951277e6effdae9f59669fb7101f6f67
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527283"
---
# <a name="spunbindrule-transact-sql"></a>sp_unbindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Disassocia una regola da una colonna o da un tipo di dati alias nel database corrente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] È consigliabile creare definizioni predefinite tramite la parola chiave DEFAULT nel [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) oppure [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) istruzioni invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_unbindrule [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @objname = ] 'object_name'` È il nome della tabella e colonna o tipo di dati alias da cui viene disassociata la regola. *object_name* viene **nvarchar(776)**, non prevede alcun valore predefinito. Tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si tenta innanzitutto di risolvere gli identificatori costituiti da due parti in nomi di colonne e quindi in tipi di dati alias. La disassociazione di una regola da un tipo di dati alias viene estesa anche alle colonne dello stesso tipo di dati a cui è applicata la regola. Non vengono tuttavia modificate le colonne di questo stesso tipo di dati a cui la regola è associata in modo diretto.  
  
> [!NOTE]  
>  *object_name* può contenere parentesi quadre **[]** come caratteri delimitatori degli identificatori. Per altre informazioni, vedere [Identificatori del database](../../relational-databases/databases/database-identifiers.md).  
  
`[ @futureonly = ] 'futureonly_flag'` Viene utilizzato solo per disassociare una regola da un tipo di dati alias. *futureonly_flag* viene **varchar(15)**, con un valore predefinito è NULL. Quando *futureonly_flag* viene **futureonly**, le colonne esistenti di tale tipo di dati non si perdono la regola specificata.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 Per visualizzare il testo di una regola, eseguire **sp_helptext** specificando il nome della regola come parametro.  
  
 Quando una regola non è associata, le informazioni sul binding vengono rimosse dal **Sys. Columns** tabella se la regola è stata associata a una colonna e dal **Sys. Types** se la regola è stata associata a un tipo di dati alias di tabella.  
  
 Una regola disassociata da un tipo di dati alias viene disassociata anche dalle colonne a cui è applicato tale tipo di dati. La regola potrebbe tuttavia rimanere associata alle colonne con tipi di dati è sono modificati successivamente tramite la clausola ALTER COLUMN di un'istruzione ALTER TABLE, è necessario disassociare la regola da queste colonne in modo specifico usando **sp_unbindrule** e specificando la nome della colonna.  
  
## <a name="permissions"></a>Permissions  
 Per disassociare una regola dalla colonna di una tabella è necessaria l'autorizzazione ALTER sulla tabella. Per disassociare una regola da un tipo di dati alias è necessaria l'autorizzazione CONTROL sul tipo di dati o l'autorizzazione ALTER sullo schema a cui appartiene il tipo.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-unbinding-a-rule-from-a-column"></a>A. Disassociazione di una regola da una colonna  
 Nell'esempio seguente la regola viene disassociata dalla colonna `startdate` di una tabella `employees`.  
  
```  
EXEC sp_unbindrule 'employees.startdate';  
```  
  
### <a name="b-unbinding-a-rule-from-an-alias-data-type"></a>B. Disassociazione di una regola da un tipo di dati alias  
 Nell'esempio seguente la regola viene disassociata dal tipo di dati alias `ssn`. La disassociazione viene applicata alle colonne di questo tipo di dati, sia esistenti che create successivamente.  
  
```  
EXEC sp_unbindrule ssn;  
```  
  
### <a name="c-using-futureonlyflag"></a>C. Utilizzo di futureonly_flag  
 Nell'esempio seguente la regola viene disassociata dal tipo di dati alias `ssn` senza influire sulle colonne `ssn` esistenti.  
  
```  
EXEC sp_unbindrule 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Utilizzo di identificatori delimitati  
 Nell'esempio seguente viene illustrato l'utilizzo di identificatori delimitati nel *object_name* parametro.  
  
```  
CREATE TABLE [t.4] (c1 int); -- Notice the period as part of the table   
-- name.  
GO  
CREATE RULE rule2 AS @value > 100;  
GO  
EXEC sp_bindrule rule2, '[t.4].c1' -- The object contains two   
-- periods; the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
GO  
EXEC sp_unbindrule '[t.4].c1';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
