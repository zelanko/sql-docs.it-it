---
title: Confronto tra GUID e valori uniqueidentifier
description: Viene illustrato come utilizzare i valori GUID e uniqueidentifier in SQL Server e .NET.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 8a4c5fcc63c2d2ddb8414227ea049e78db1cba10
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452287"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>Confronto tra GUID e valori uniqueidentifier

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Il tipo di dati identificatore univoco globale (GUID) in SQL Server è rappresentato dal tipo di dati `uniqueidentifier`, che archivia un valore binario a 16 byte. Un GUID è un numero binario e il suo utilizzo principale è costituito da un identificatore che deve essere univoco in una rete con molti computer in molti siti. I GUID possono essere generati chiamando la funzione NEWID Transact-SQL e sono sicuramente univoci in tutto il mondo. Per ulteriori informazioni, vedere [uniqueidentifier (Transact-SQL)](../../../t-sql/data-types/uniqueidentifier-transact-sql.md).  
  
## <a name="working-with-sqlguid-values"></a>Uso dei valori di SqlGuid  
Poiché i valori dei GUID sono lunghi e nascosti, non sono significativi per gli utenti. Se vengono usati GUID generati casualmente per i valori di chiave e si inseriscono numerose righe, si ottengono I/O casuali negli indici, che possono influire negativamente sulle prestazioni. I GUID sono inoltre relativamente grandi rispetto ad altri tipi di dati. In generale, è consigliabile usare i GUID solo per scenari molto ristretti per i quali non è adatto nessun altro tipo di dati.  
  
### <a name="comparing-guid-values"></a>Confronto di valori GUID  
Con valori `uniqueidentifier` è possibile usare gli operatori di confronto. Quando si confrontano gli schemi di bit dei due valori, tuttavia, l'ordinamento non viene implementato. Le uniche operazioni consentite su un valore `uniqueidentifier` sono i confronti (=, <>, \<, >, \<=, >=) e il controllo di valori NULL (IS NULL e IS NOT NULL). Non sono consentiti altri operatori aritmetici.  
  
Sia <xref:System.Guid> che <xref:System.Data.SqlTypes.SqlGuid> hanno un metodo `CompareTo` per confrontare valori GUID diversi. Tuttavia, `System.Guid.CompareTo` e `SqlTypes.SqlGuid.CompareTo` sono implementate in modo diverso. <xref:System.Data.SqlTypes.SqlGuid> implementa `CompareTo` utilizzando il comportamento SQL Server negli ultimi sei byte di un valore sono più significativi. <xref:System.Guid> valuta tutti i 16 byte. L'esempio seguente illustra queste differenze di comportamento. Nella prima sezione del codice vengono visualizzati i valori di <xref:System.Guid> non ordinati e la seconda sezione del codice mostra i valori <xref:System.Guid> ordinati. La terza sezione Mostra i valori <xref:System.Data.SqlTypes.SqlGuid> ordinati. L'output viene visualizzato sotto il listato di codice.  
  
[!code-csharp[DataWorks SqlGuid#1](~/../sqlclient/doc/samples/SqlGuid.cs#1)]
  
L'esempio produce i risultati seguenti.  
  
```console
Unsorted Guids:  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
  
Sorted Guids:  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
  
Sorted SqlGuids:  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
```  
  
## <a name="next-steps"></a>Passaggi successivi
- [Tipi di dati SQL Server e ADO.NET](sql-server-data-types.md)
