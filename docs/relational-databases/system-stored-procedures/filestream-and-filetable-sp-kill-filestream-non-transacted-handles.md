---
title: sp_kill_filestream_non_transacted_handles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7189499084c40d297f30514ba2f9bf5c01ada510
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52397644"
---
# <a name="spkillfilestreamnontransactedhandles-transact-sql"></a>sp_kill_filestream_non_transacted_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di chiudere handle di file non transazionali per dati di tabelle FileTable.  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] 'table_name', [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *table_name*  
 Nome della tabella in cui chiudere handle non transazionali.  
  
 È possibile passare *nome_tabella* senza *handle_id* per chiudere handle non transazionali aperti tutti per la tabella FileTable.  
  
 È possibile passare NULL per il valore della *table_name* per chiudere handle non transazionali aperti tutti per tutte le tabelle Filetable nel database corrente. Il valore predefinito è NULL.  
  
 *handle_id*  
 ID facoltativo del singolo handle da chiudere. È possibile ottenere il *handle_id* dalle [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) vista a gestione dinamica. Ogni ID è univoco in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si specifica *handle_id*, quindi è necessario anche specificare un valore per *table_name*.  
  
 È possibile passare NULL per il valore della *handle_id* per chiudere handle non transazionali aperti tutti per la tabella FileTable specificata da *table_name*. Il valore predefinito è NULL.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-set"></a>Set di risultati  
 Nessuna.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Il *handle_id* richiesto dal **sp_kill_filestream_non_transacted_handles** non è correlato a session_id o all'unità di lavoro che viene usato in altri **kill** comandi.  
  
 Per altre informazioni, vedere [Gestire le tabelle FileTable](../../relational-databases/blob/manage-filetables.md).  
  
## <a name="metadata"></a>Metadati  
 Per informazioni sugli handle di file non transazionali aperti, eseguire una query nella vista a gestione dinamica [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 È necessario disporre **VIEW DATABASE STATE** dell'autorizzazione per ottenere gli handle di file dalle **sys.dm_FILESTREAM_non_transacted_handles** vista a gestione dinamica e l'esecuzione **sp_kill_filestream_non_ transacted_handles**.  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti illustrano come chiamare **sp_kill_filestream_non_transacted_handles** per chiudere handle di file non transazionali per dati di tabelle FileTable.  
  
```sql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable'  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable', @handle_id = 0xFFFAAADD  
```  
  
 Nell'esempio seguente viene illustrato come utilizzare uno script per ottenere un *handle_id* e chiuderlo.  
  
```sql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire tabelle FileTable](../../relational-databases/blob/manage-filetables.md)  
 [FileStream e viste a gestione dinamica FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
 <br>[FileStream e viste del catalogo FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
 <br>[sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
