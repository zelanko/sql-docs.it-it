---
title: Accedere a Dati FILESTREAM con Transact-SQL| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Transact-SQL
ms.assetid: a6bf0ce7-7e5e-4a07-8917-ee526c9d0a05
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 067f14e857addc5f43a0b17d81d554997adbc09f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010435"
---
# <a name="access-filestream-data-with-transact-sql"></a>Accedere a Dati FILESTREAM con Transact-SQL
  Questo argomento descrive come usare le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT, UPDATE e DELETE per gestire dati FILESTREAM.  
  
> [!NOTE]  
>  Gli esempi riportati in questo argomento richiedono il database e la tabella abilitati per FILESTREAM creati in [Creare un database abilitato per FILESTREAM](create-a-filestream-enabled-database.md) e [Creare una tabella per archiviare dati FILESTREAM](create-a-table-for-storing-filestream-data.md).  
  
##  <a name="ins"></a> Inserimento di una riga che contiene dati FILESTREAM  
 Per aggiungere una riga a una tabella che supporta i dati FILESTREAM, utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT. Quando vengono inseriti dati in una colonna FILESTREAM, è possibile inserire NULL o un valore `varbinary(max)`.  
  
### <a name="inserting-null"></a>Inserimento di NULL  
 Nell'esempio seguente viene illustrato come inserire il valore `NULL`. Se il valore FILESTREAM è `NULL`, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non crea alcun file nel file system.  
  
 [!code-sql[FILESTREAM#FS_InsertNULL](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertnull)]  
  
### <a name="inserting-a-zero-length-record"></a>Inserimento di un record di lunghezza zero  
 Nell'esempio seguente viene illustrato l'utilizzo di `INSERT` per creare un record di lunghezza zero. Questa istruzione risulta utile quando si desidera ottenere un handle di file, ma si modifica il file utilizzando API Win32.  
  
 [!code-sql[FILESTREAM#FS_InsertZero](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertzero)]  
  
### <a name="creating-a-data-file"></a>Creazione di un file di dati  
 Nell'esempio seguente viene illustrato l'utilizzo di `INSERT` per creare un file contenente dati. Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] converte la stringa `Seismic Data` in un valore `varbinary(max)` . Se non esiste già, FILESTREAM crea il file di Windows. I dati verranno quindi aggiunti al file di dati.  
  
 [!code-sql[FILESTREAM#FS_InsertData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertdata)]  
  
 Se si selezionano tutti i dati della tabella `Archive`,`dbo.Records` i risultati dovrebbero essere analoghi a quelli illustrati nella tabella seguente. La colonna `Id` conterrà tuttavia GUID diversi.  
  
|ID|SerialNumber|Riprendi|  
|--------|------------------|------------|  
|`C871B90F-D25E-47B3-A560-7CC0CA405DAC`|`1`|`NULL`|  
|`F8F5C314-0559-4927-8FA9-1535EE0BDF50`|`2`|`0x`|  
|`7F680840-B7A4-45D4-8CD5-527C44D35B3F`|`3`|`0x536569736D69632044617461`|  
  
##  <a name="upd"></a> Aggiornamento di dati FILESTREAM  
 Per aggiornare i dati in file del file system, è possibile usare [!INCLUDE[tsql](../../includes/tsql-md.md)] , sebbene sia preferibile evitare questa procedura quando si devono trasmettere elevate quantità di dati a un file.  
  
 Nel seguente esempio il testo nel record del file viene sostituito con il testo `Xray 1`.  
  
 [!code-sql[FILESTREAM#FS_UpdateData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_updatedata)]  
  
##  <a name="del"></a> Eliminazione di dati FILESTREAM  
 Quando si elimina una riga che contiene un campo FILESTREAM, vengono eliminati anche i file del file system sottostanti. L'unico modo per eliminare una riga e pertanto il file è l'utilizzo dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] DELETE.  
  
 Nell'esempio seguente viene descritta l'eliminazione di una riga e dei file del file system associati.  
  
 [!code-sql[FILESTREAM#FS_DeleteData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_deletedata)]  
  
 Se si selezionano tutti i dati della tabella `dbo.Archive` , si nota che la riga non è più presente. Non è più possibile utilizzare il file associato.  
  
> [!NOTE]  
>  I file sottostanti vengono rimossi dal Garbage Collector di FILESTREAM.  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare e configurare FILESTREAM](enable-and-configure-filestream.md)   
 [Evitare conflitti con le operazioni del database nelle applicazioni di FILESTREAM](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
