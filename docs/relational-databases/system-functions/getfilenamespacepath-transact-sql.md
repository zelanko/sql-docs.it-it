---
title: GetFileNamespacePath (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- GetFileNamespacePath
- GetFileNamespacePath_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetFileNamespacePath function
ms.assetid: b393ecef-baa8-4d05-a268-b2f309fce89a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9c94fc80bd516c0be5b414aac98e0e4435ec8b53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628082"
---
# <a name="getfilenamespacepath-transact-sql"></a>GetFileNamespacePath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce il percorso UNC per un file o una directory in una tabella FileTable.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<column-name>.GetFileNamespacePath(is_full_path, @option)  
```  
  
## <a name="arguments"></a>Argomenti  
 *column-name*  
 Il nome della colonna del varbinary (max) **file_stream** in una tabella FileTable.  
  
 Il *-nome della colonna* valore deve essere un nome di colonna valido. Non può essere un'espressione o un valore convertito o di cui sia stato eseguito il cast da una colonna di un altro tipo di dati.  
  
 *is_full_path*  
 Espressione Integer che specifica se restituire un percorso relativo o assoluto. *is_full_path* può avere uno dei valori seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Restituisce il percorso relativo all'interno della directory a livello di database.<br /><br /> Si tratta del valore predefinito.|  
|**1**|Restituisce il percorso UNC completo, che inizia con `\\computer_name`.|  
  
 *@option*  
 Espressione Integer che definisce la formattazione del componente server del percorso. *@option* Può avere uno dei valori seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Restituisce il nome del server convertito in formato NetBIOS, ad esempio:<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> Rappresenta il valore predefinito.|  
|**1**|Restituisce il nome del server senza conversione, ad esempio:<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|Restituisce il percorso completo del server, ad esempio:<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>Tipo restituito  
 **nvarchar(max)**  
  
 Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fa parte di un cluster di failover, il nome computer restituito come parte di questo percorso è il nome host virtuale per l'istanza cluster.  
  
 Quando il database appartiene a un gruppo di disponibilità Always On, il **FileTableRootPath** funzione restituisce il nome di rete virtuale (VNN) invece del nome computer.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Il percorso che il **GetFileNamespacePath** funzione restituisce un percorso di directory o file logico nel formato seguente:  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\...`  
  
 Questo percorso logico non corrisponde direttamente a un percorso NTFS fisico. Viene convertito al percorso fisico dal driver del filtro del FILESTREAM file system e l'agente di FILESTREAM. La separazione tra percorso logico e percorso fisico consente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di riorganizzare i dati internamente senza incidere sulla validità del percorso.  
  
## <a name="best-practices"></a>Procedure consigliate  
 Per mantenere il codice e le applicazioni indipendenti dal database e dal computer correnti, evitare di scrivere codice basato su percorsi di file assoluti. Ottenere invece il percorso completo di un file in fase di esecuzione usando il **FileTableRootPath** e **GetFileNamespacePath** funzioni insieme, come illustrato nell'esempio seguente. Per impostazione predefinita, la funzione **GetFileNamespacePath** restituisce il percorso relativo del file all'interno del percorso radice per il database.  
  
```sql  
USE MyDocumentDatabase;  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
  
@fullPath = varchar(1000);  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath() FROM DocumentStore  
WHERE Name = N'document.docx';  
```  
  
## <a name="remarks"></a>Note  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti illustrano come chiamare le **GetFileNamespacePath** funzione per ottenere il percorso UNC per un file o directory in una tabella FileTable.  
  
```  
-- returns the relative path of the form "\MyFileTable\MyDocDirectory\document.docx"  
SELECT file_stream.GetFileNamespacePath() AS FilePath FROM DocumentStore  
WHERE Name = N'document.docx';  
  
-- returns "\\MyServer\MSSQLSERVER\MyDocumentDatabase\MyFileTable\MyDocDirectory\document.docx"  
SELECT file_stream.GetFileNamespacePath(1, Null) AS FilePath FROM DocumentStore  
WHERE Name = N'document.docx';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Usare directory e percorsi in FileTable](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
