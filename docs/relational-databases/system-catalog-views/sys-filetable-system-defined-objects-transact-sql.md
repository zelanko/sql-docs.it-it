---
title: sys. filetable_system_defined_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.filetable_system_defined_objects_TSQL
- filetable_system_defined_objects
- filetable_system_defined_objects_TSQL
- sys.filetable_system_defined_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetable_system_defined_objects catalog view
ms.assetid: 62022e6b-46f6-495f-b14b-53f41e040361
author: stevestein
ms.author: sstein
ms.openlocfilehash: dd05f24ab90844065b708230ee016ce9ce78bfbd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68005156"
---
# <a name="sysfiletable_system_defined_objects-transact-sql"></a>sys.filetable_system_defined_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contiene un elenco degli oggetti definiti dal sistema correlati a tabelle FileTable. Contiene una riga per ogni oggetto definito dal sistema.  
  
 Quando si crea una tabella FileTable, vengono creati contemporaneamente anche gli oggetti correlati, quali vincoli e indici. Non è possibile modificare o eliminare questi oggetti, che verranno eliminato solo all'eliminazione della tabella FileTable stessa.  
  
 Per altre informazioni sugli oggetti FileTable, vedere [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
|Colonna|Tipo di dati|Descrizione|  
|------------|---------------|-----------------|  
|**object_id**|**int**|ID dell'oggetto definito dal sistema correlato a una tabella FileTable.<br /><br /> Fa riferimento all'oggetto in **sys. Objects**.|  
|**parent_object_id**|**int**|ID oggetto della tabella FileTable padre.<br /><br /> Fa riferimento all'oggetto in **sys. Objects**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creare, modificare ed eliminare FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [Gestione di tabelle FileTable](../../relational-databases/blob/manage-filetables.md)  
  
  
