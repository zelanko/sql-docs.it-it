---
description: Write (Motore di database)
title: Write (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Write_TSQL
- Write
dev_langs:
- TSQL
helpviewer_keywords:
- Write [Database Engine]
ms.assetid: 7c554334-d2d9-4eae-a4ae-097aa4020e1a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: eb08d6f4d10a5cdf0047022185e24828b3ae37b5
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "92037454"
---
# <a name="write-database-engine"></a>Write (Motore di database)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Write scrive una rappresentazione binaria di **SqlHierarchyId** nell'oggetto **BinaryWriter** passato. Write non può essere chiamato usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Utilizzare invece CAST o CONVERT.
  
## <a name="syntax"></a>Sintassi  
  
```csharp
void Write( BinaryWriter w )
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
*w*  
Oggetto **BinaryWriter** su cui verrà scritta la rappresentazione binaria di questo nodo **hierarchyid**.
  
## <a name="return-types"></a>Tipi restituiti  
**Tipo CLR restituito: void**
  
## <a name="remarks"></a>Osservazioni  
Write viene usato internamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando è necessario, ad esempio in caso di caricamento di dati da una colonna **hierarchyid**. Write viene anche chiamato internamente in caso di esecuzione di una conversione tra **hierarchyid** e **varbinary**.
  
## <a name="examples"></a>Esempi  
  
```csharp
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
```  
  
## <a name="see-also"></a>Vedere anche
[Read &#40;motore di database&#41;](../../t-sql/data-types/read-database-engine.md)  
[ToString &#40;motore di database&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Guida di riferimento ai metodi per il tipo di dati hierarchyid](./hierarchyid-data-type-method-reference.md)
  
