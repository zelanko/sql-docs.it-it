---
title: Suggerimenti per l'ordinamento per operazioni di copia bulk
description: Descrive come usare suggerimenti per l'ordinamento nelle operazioni di copia bulk.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: c7365bdc6da75e04d019ca1a6a87b90dd8d4ec3c
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85110182"
---
# <a name="order-hints-for-bulk-copy-operations"></a>Suggerimenti per l'ordinamento per operazioni di copia bulk

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Le operazioni di copia bulk offrono vantaggi significativi in termini di prestazioni rispetto ad altri metodi per il caricamento di dati in una tabella di SQL Server. Le prestazioni possono essere ulteriormente migliorate usando suggerimenti per l'ordinamento. Specificando suggerimenti per l'ordinamento per le operazioni di copia bulk, è possibile ridurre i tempi di inserimento di dati ordinati in tabelle con indici cluster.

Per impostazione predefinita, l'operazione di inserimento bulk presuppone che i dati non siano ordinati. SQL Server forza un ordinamento intermedio dei dati prima del caricamento bulk. Se si è certi che i dati in ingresso sono già ordinati, è possibile usare suggerimenti per l'ordinamento per indicare all'operazione di copia bulk l'ordinamento di qualsiasi colonna di destinazione che fa parte di un indice cluster.
  
## <a name="adding-order-hints-to-a-bulk-copy-operation"></a>Aggiunta di suggerimenti per l'ordinamento a un'operazione di copia bulk  
L'esempio seguente esegue la copia bulk di dati da una tabella di origine nel database di esempio **AdventureWorks** a una tabella di destinazione nello stesso database. Viene creato un oggetto SqlBulkCopyColumnOrderHint per definire il tipo di ordinamento per la colonna **ProductNumber** nella tabella di destinazione. Il suggerimento per l'ordinamento viene quindi aggiunto all'istanza di SqlBulkCopy, che aggiungerà l'argomento del suggerimento per l'ordinamento appropriato alla query `INSERT BULK` risultante.

[!code-csharp [SqlBulkCopy.ColumnOrderHint#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnOrderHint.cs#1)]

## <a name="next-steps"></a>Passaggi successivi
- [Operazioni di copia bulk in SQL Server](bulk-copy-operations-sql-server.md)
