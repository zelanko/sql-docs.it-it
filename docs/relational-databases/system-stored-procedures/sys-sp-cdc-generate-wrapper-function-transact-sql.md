---
title: Sys. sp_cdc_generate_wrapper_function (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_generate_wrapper_function_TSQL
- sp_cdc_generate_wrapper_function
- sys.sp_cdc_generate_wrapper_function_TSQL
- sys.sp_cdc_generate_wrapper_function
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_generate_wrapper_function
- sp_cdc_generate_wrapper_function
ms.assetid: 85bc086d-8a4e-4949-a23b-bf53044b925c
author: rothja
ms.author: jroth
ms.openlocfilehash: 074e114f81db6615a04240f10447a3f711a51cf7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083747"
---
# <a name="sysspcdcgeneratewrapperfunction-transact-sql"></a>sys.sp_cdc_generate_wrapper_function (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera script per creare funzioni wrapper per funzioni di query Change Data Capture disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'API è supportata nei wrapper generati consente l'intervallo di query specificare come un intervallo di data/ora. In questo modo la funzione può essere utilizzata in molte applicazioni di data warehousing, incluse quelle sviluppate da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] finestre di progettazione di pacchetti che usano change data capture tecnologia per determinare il carico incrementale.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.sp_cdc_generate_wrapper_function  
    [ [ @capture_instance sysname = ] 'capture_instance'  
    [ , [ @closed_high_end_point = ] closed_high_end_pt  
    [ , [ @column_list = ] 'column_list'  
```  
  
```  
  
[ , [ @update_flag_list = ] 'update_flag_list'  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @capture_instance=] '*capture_instance*'  
 Istanza di acquisizione per la quale gli script devono essere generati. *capture_instance* viene **sysname** e ha un valore predefinito null. Se il valore viene omesso oppure viene impostato in modo esplicito su NULL, gli script del wrapper vengono generati per tutte le istanze di acquisizione  
  
 [ @closed_high_end_point=] *high_end_pt_flag*  
 Flag che indica se modifiche per cui l'ora di commit è uguale all'endpoint superiore devono essere incluse nell'intervallo di estrazione dalla routine generata. *high_end_pt_flag* viene **bit** e ha un valore predefinito di 1, che indica che l'endpoint deve essere incluso. Il valore 0 indica che tutte le ore di commit saranno minori dell'endpoint superiore.  
  
 [ @column_list=] '*column_list*'  
 Elenco di colonne acquisite da includere nel set di risultati restituito dalla funzione wrapper. *column_list* viene **nvarchar (max)** e ha un valore predefinito null. Si si specifica NULL, vengono incluse tutte le colonne acquisite.  
  
 [ @update_flag_list=] '*update_flag_list*'  
 Elenco di colonne incluse per cui viene inserito un flag nel set di risultati restituiti dalla funzione wrapper. *update_flag_list* viene **nvarchar (max)** e ha un valore predefinito null. Se si specifica NULL, non viene incluso alcun flag.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di colonna|Descrizione|  
|-----------------|-----------------|-----------------|  
|**function_name**|**nvarchar(145)**|Nome della funzione generata.|  
|**create_script**|**nvarchar(max)**|Script che crea la funzione wrapper relativa all'istanza di acquisizione.|  
  
## <a name="remarks"></a>Note  
 Lo script che crea la funzione per eseguire il wrapping delle query relative a tutte le modifiche per un'istanza di acquisizione viene sempre generato. Se l'istanza di acquisizione supporta query relative alle modifiche totali, lo script per generare un wrapper per tale tipo di query viene comunque creato.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come utilizzare `sys.sp_cdc_generate_wrapper_function` per creare wrapper per tutte le funzioni di Change Data Capture.  
  
```  
DECLARE @wrapper_functions TABLE (  
    function_name sysname,  
    create_script nvarchar(max));  
  
INSERT INTO @wrapper_functions  
EXEC sys.sp_cdc_generate_wrapper_function;  
  
DECLARE @create_script nvarchar(max);  
DECLARE #hfunctions CURSOR LOCAL fast_forward  
FOR   
    SELECT create_script FROM @wrapper_functions;  
  
OPEN #hfunctions;  
FETCH #hfunctions INTO @create_script;  
WHILE (@@fetch_status <> -1)  
BEGIN  
    EXEC sp_executesql @create_script  
    FETCH #hfunctions INTO @create_script  
END;  
  
CLOSE #hfunctions;  
DEALLOCATE #hfunctions;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure Change Data Capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Change Data Capture &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)  
  
  
