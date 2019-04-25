---
title: sp_db_selective_xml_index (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_selective_xml_index_TSQL
- sp_db_selective_xml_index
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_selective_xml_index procedure
ms.assetid: 017301a2-4a23-4e68-82af-134f3d4892b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e9b1752b5e567c2a26080422874e5bf6e31bc568
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506691"
---
# <a name="spdbselectivexmlindex-transact-sql"></a>sp_db_selective_xml_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Abilita e disabilita la funzionalità degli indici XML selettivi in un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se chiamata senza parametri, la stored procedure restituisce 1 se l'indice XML selettivo è abilitato in un database specifico.  
  
> [!NOTE]  
>  Per disabilitare l'indice XML selettivo tramite questa stored procedure, il database deve essere riportato in modalità di recupero con registrazione minima utilizzando il [opzioni ALTER DATABASE SET &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) comando.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
  
      sys.sp_db_selective_xml_index[[ @db_name = ] 'db_name'],   
[[ @action = ] 'action']  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @ db_name = ] 'db_name'` Il nome del database per abilitare o disabilitare l'indice XML selettivo in. Se *db_name* è NULL, si presuppone che il database corrente.  
  
`[ @action = ] 'action'` Determina se abilitare o disabilitare l'indice. Se un altro valore ad eccezione del fatto 'on', 'true', 'off' o 'false' è passato, verrà generato un errore.  
  
```  
  
Allowed values: 'on', 'off', 'true', 'false'  
```  
  
## <a name="return-code-values"></a>Valori restituiti  
 **1** se l'indice XML selettivo è abilitato in un database specifico.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-enable-selective-xml-index-functionality"></a>A. Abilitare la funzionalità degli indici XML selettivi  
 Nell'esempio seguente viene abilitato l'indice XML selettivo nel database corrente.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'on';  
GO  
```  
  
 Nell'esempio seguente viene abilitato l'indice XML selettivo nel database AdventureWorks2012.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'true';  
GO  
```  
  
### <a name="b-disable-selective-xml-index-functionality"></a>B. Disabilitare la funzionalità degli indici XML selettivi  
 Nell'esempio seguente viene disabilitato l'indice XML selettivo nel database corrente.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'off';  
GO  
```  
  
 Nell'esempio seguente viene disabilitato l'indice XML selettivo nel database AdventureWorks2012.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'false';  
GO  
```  
  
### <a name="c-detect-if-selective-xml-index-is-enabled"></a>C. Rilevare se l'indice XML selettivo è abilitato  
 Nell'esempio seguente viene rilevato se l'indice XML selettivo è abilitato. Restituisce 1 se l'indice XML selettivo è abilitato.  
  
```  
EXECUTE sys.sp_db_selective_xml_index;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Indici XML selettivi &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
