---
title: Read (Motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7aa7978fb568eafc62060130c4e8220f4d5612dd
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56037522"
---
# <a name="read-database-engine"></a>Read (Motore di database)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Read legge la rappresentazione binaria di **SqlHierarchyId** dall'elemento passato **BinaryReader** e imposta l'oggetto **SqlHierarchyId** su tale valore. Read non può essere chiamato tramite [!INCLUDE[tsql](../../includes/tsql-md.md)]. Utilizzare invece CAST o CONVERT.
  
## <a name="syntax"></a>Sintassi  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>Argomenti  
*r*  
 Oggetto **BinaryReader** che produce un flusso binario corrispondente a una rappresentazione binaria di un nodo **hierarchyid**.  
  
## <a name="return-types"></a>Tipi restituiti
 **Tipo CLR restituito: void**  
  
## <a name="remarks"></a>Remarks  
 Read non esegue la convalida dell'input. Se viene specificato un input binario non valido, Read può generare un'eccezione oppure può avere esito positivo ma restituire un oggetto **SqlHierarchyId** non valido i cui metodi possono restituire risultati imprevisti o generare un'eccezione.  
  
 Read può essere chiamato solo su un oggetto **SqlHierarchyId** appena creato.  
  
 Read viene usato internamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando è necessario, ad esempio in caso di scrittura di dati in una colonna **hierarchyid**. Read viene anche chiamato internamente in caso di esecuzione di una conversione tra **varbinary** e **hierarchyid**.  
  
## <a name="examples"></a>Esempi  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>Vedere anche  
[Write &#40;Motore di database&#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40;motore di database&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Guida di riferimento ai metodi per il tipo di dati hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
