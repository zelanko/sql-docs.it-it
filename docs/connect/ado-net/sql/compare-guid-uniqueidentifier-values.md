---
title: Confronto tra GUID e valori uniqueidentifier
description: Viene illustrato come usare i valori GUID e uniqueidentifier in SQL Server e .NET.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 35fc93a9ce6eb5b1709c6671adb21eb3030dea63
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247845"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>Confronto tra GUID e valori uniqueidentifier

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Il tipo di dati identificatore univoco globale (GUID, Globally Unique IDentifier) in SQL Server è rappresentato dal tipo di dati `uniqueidentifier`, in cui è archiviato un valore binario di 16 byte. Un GUID è un numero binario usato principalmente come identificatore univoco in una rete con molti computer in più siti. I GUID possono essere generati chiamando la funzione NEWID di Transact-SQL. Si assicura l'univocità in tutto il mondo. Per altre informazioni, vedere [uniqueidentifier (Transact-SQL)](../../../t-sql/data-types/uniqueidentifier-transact-sql.md).  
  
## <a name="working-with-sqlguid-values"></a>Uso di valori SqlGuid  
I GUID sono valori lunghi e poco chiari, pertanto molti utenti non ne comprendono il significato. Se si usano GUID generati in modo casuale per valori chiave e se si inserisce un numero elevato di righe, l'I/O negli indici sarà casuale, determinando un impatto negativo sulle prestazioni. Rispetto ad altri tipo di dati, i GUID sono anche valori relativamente grandi. È in genere consigliabile usare i GUID solo per pochi scenari, nei quali non sono adatti altri tipi di dati.  
  
### <a name="comparing-guid-values"></a>Confronto di valori GUID  
Con valori `uniqueidentifier` è possibile usare gli operatori di confronto. Quando si confrontano gli schemi di bit dei due valori, tuttavia, l'ordinamento non viene implementato. Le uniche operazioni consentite su un valore `uniqueidentifier` sono i confronti (=, <>, \<, >, \<=, >=) e il controllo di valori NULL (IS NULL e IS NOT NULL). Non sono ammessi altri operatori aritmetici.  
  
Sia <xref:System.Guid> che <xref:System.Data.SqlTypes.SqlGuid> usano un metodo `CompareTo` per confrontare valori GUID diversi. `System.Guid.CompareTo` e `SqlTypes.SqlGuid.CompareTo` sono tuttavia implementati in modo diverso. <xref:System.Data.SqlTypes.SqlGuid> implementa `CompareTo` usando il comportamento di SQL Server, in cui gli ultimi 6 byte di un valore sono i più significativi. <xref:System.Guid> valuta tutti i 16 byte. L'esempio seguente illustra queste differenze di comportamento. La prima sezione del codice visualizza valori <xref:System.Guid> non ordinati, mentre la seconda sezione visualizza i valori <xref:System.Guid> ordinati. La terza sezione visualizza i valori <xref:System.Data.SqlTypes.SqlGuid> ordinati. L'output viene visualizzato sotto l'elenco codici.  
  
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
