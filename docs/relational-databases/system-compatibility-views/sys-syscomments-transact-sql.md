---
title: sys.syscomments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscomments_TSQL
- syscomments
- syscomments_TSQL
- sys.syscomments
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscomments compatibility view
- syscomments system table
ms.assetid: 767dd410-6bc9-4c4a-ab0f-6d2cf6163426
author: rothja
ms.author: jroth
ms.openlocfilehash: 183fa2fc1a674ec1cc987c265f5a0d4c399e27cc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68010753"
---
# <a name="syssyscomments-transact-sql"></a>sys.syscomments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene voci per ogni vista, regola, valore predefinito, trigger, vincolo CHECK, vincolo DEFAULT e stored procedure all'interno di un database. La colonna di **testo** contiene le istruzioni di definizione SQL originali.  
  
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] È consigliabile utilizzare in alternativa i moduli sys.sql. Per ulteriori informazioni, vedere [sys. sql_modules &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**ID**|**int**|ID di oggetto a cui si riferisce il testo.|  
|**number**|**smallint**|Numero all'interno del gruppo di procedure, se raggruppate.<br /><br /> 0 = Le voci immesse non sono procedure.|  
|**colid**|**smallint**|Numero di sequenza di riga per definizioni di oggetto con più di 4.000 caratteri.|  
|**stato**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**CTEXT**|**varbinary (8000)**|Byte non elaborati dell'istruzione di definizione SQL.|  
|**texttype**|**smallint**|0 = Commento fornito dall'utente.<br /><br /> 1 = Commento fornito dal sistema.<br /><br /> 4 = Commento crittografato.|  
|**linguaggio**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**crittografati**|**bit**|Indica se la definizione della stored procedure è offuscata.<br /><br /> 0 = Non offuscata<br /><br /> 1 = Offuscata<br /><br /> ** \* Importante \* \* ** Per offuscare le definizioni di stored procedure, utilizzare CREATE PROCEDURE con la parola chiave ENCRYPTION.|  
|**compressi**|**bit**|Restituisce sempre 0. Indica che la procedura è compressa.|  
|**text**|**nvarchar(4000)**|Testo effettivo dell'istruzione di definizione SQL.<br /><br /> La semantica dell'espressione decodificata è equivalente al testo originale, tuttavia non è garantito che la sintassi venga mantenuta. Gli spazi vuoti vengono ad esempio eliminati dall'espressione decodificata.<br /><br /> Questa [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]vista compatibile con ottiene informazioni dalle strutture correnti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e può restituire più caratteri della definizione **nvarchar (4000)** . **sp_help** restituisce **nvarchar (4000)** come tipo di dati della colonna di testo. Quando si lavora con **syscomments** , è consigliabile usare **nvarchar (max)**. Per le nuove attività di sviluppo, non usare **syscomments**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste di compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
