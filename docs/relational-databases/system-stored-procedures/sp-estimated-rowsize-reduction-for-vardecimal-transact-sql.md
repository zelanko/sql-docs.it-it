---
title: sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- sp_estimated_rowsize_reduction_for_vardecimal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- decimal data type, compressing
- numeric data type, compressing
- estimate decimal compression
- table compression [SQL Server]
ms.assetid: 0fe45983-f9f2-4c7f-938a-0fd96e1cbe8d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 90de7b95febdf2f1a25a5e584b2ca77bb67f93d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124506"
---
# <a name="spestimatedrowsizereductionforvardecimal-transact-sql"></a>sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stima la riduzione delle dimensioni medie delle righe se in una tabella viene abilitato il formato di archiviazione vardecimal. Utilizzare questo numero per stimare la riduzione complessiva delle dimensioni della tabella. Poiché per calcolare la riduzione media delle dimensioni delle righe viene utilizzato il campionamento statistico, i risultati ottenuti devono essere considerati esclusivamente come una stima. In rari casi è possibile che le dimensioni delle righe aumentino dopo l'abilitazione del formato di archiviazione vardecimal.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Utilizzare preferibilmente la compressione di riga e di pagina. Per altre informazioni, vedere [Data Compression](../../relational-databases/data-compression/data-compression.md). Per gli effetti di compressione per le dimensioni di tabelle e indici, vedere [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_estimated_rowsize_reduction_for_vardecimal [ [ @table_name = ] 'table'] [;]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @table = ] 'table'` È il nome in tre parti della tabella per cui è necessario modificare il formato di archiviazione. *Nella tabella* viene **nvarchar(776)** .  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Per offrire informazioni sulle dimensioni correnti e stimate della tabella, viene restituito il set di risultati seguente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**avg_rowlen_fixed_format**|**numero decimale (12, 2)**|Rappresenta la lunghezza della riga nel formato di archiviazione decimal fisso.|  
|**avg_rowlen_vardecimal_format**|**numero decimale (12, 2)**|Rappresenta le dimensioni medie delle righe in caso di utilizzo del formato di archiviazione vardecimal.|  
|**row_count**|**int**|Numero di righe nella tabella.|  
  
## <a name="remarks"></a>Note  
 Uso **sp_estimated_rowsize_reduction_for_vardecimal** per stimare il risparmio risultante se si abilita il formato di archiviazione vardecimal per una tabella. Se, ad esempio, le dimensioni medie della riga possono essere ridotte del 40%, è possibile ridurre del 40% le dimensioni della tabella. Si potrebbe non ottenere un risparmio in termini di spazio a seconda del fattore di riempimento e delle dimensioni della riga. Se, ad esempio, si riducono del 40% le dimensioni di una riga lunga 8000 byte, una pagina di dati può comunque contenere una sola riga, pertanto non si hanno risparmi in termini di spazio.  
  
 Se i risultati della **sp_estimated_rowsize_reduction_for_vardecimal** indicano che la tabella si espanderà, ciò significa che molte righe della tabella usano quasi la precisione completa dei tipi di dati decimali e l'aggiunta del limitato overhead aggiuntivo necessario per il formato di archiviazione vardecimal è supera il risparmio garantito da tale formato. In questi rari casi, non abilitare il formato di archiviazione vardecimal.  
  
 Se una tabella è abilitata per il formato di archiviazione vardecimal, utilizzare **sp_estimated_rowsize_reduction_for_vardecimal** per stimare le dimensioni medie della riga se il formato di archiviazione vardecimal è disabilitato.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CONTROL per la tabella.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene stimata la riduzione delle dimensioni delle righe in caso di compressione della tabella `Production.WorkOrderRouting` del database `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimated_rowsize_reduction_for_vardecimal 'Production.WorkOrderRouting' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_db_vardecimal_storage_format &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
