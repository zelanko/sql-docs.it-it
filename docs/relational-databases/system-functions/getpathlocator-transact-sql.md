---
title: GetPathLocator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
author: rothja
ms.author: jroth
ms.openlocfilehash: 4cec490522f8bacc774213ec1af5cce1af0eefef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910250"
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce il valore dell'ID localizzatore del percorso per la directory o il file specificato in una tabella FileTable.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>Argomenti  
 *filenamespace_path*  
 Percorso dello spazio dei nomi nella tabella FileTable. Il percorso dello spazio dei nomi JE typu **nvarchar (max)** .  
  
 Quando il database appartiene a un gruppo di disponibilità Always On, il **GetPathLocator** funzione accetta il nome di rete virtuale (VNN) o il nome del computer.  
  
## <a name="return-type"></a>Tipo restituito  
 **hierarchyid**  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Per altre informazioni, vedere [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
## <a name="examples"></a>Esempi  
 È possibile usare la **GetPathLocator** funzionare quando si è la migrazione dei file da un file server a una tabella FileTable. In questo scenario si desidera spostare i file nella tabella FileTable, quindi sostituire il percorso UNC originale per ogni file con il percorso UNC della tabella FileTable. Per un esempio completo, vedere [caricare file in Filetable](../../relational-databases/blob/load-files-into-filetables.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Usare directory e percorsi in FileTable](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
