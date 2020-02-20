---
title: Più operazioni di copia bulk
description: Viene descritto come eseguire più operazioni di copia bulk dei dati in un'istanza di SQL Server usando la classe SqlBulkCopy.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5ad12f94-7459-4a93-a421-4160d1a90715
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 423300788a020a18914a5bd25abac379cbb71500
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247694"
---
# <a name="multiple-bulk-copy-operations"></a>Più operazioni di copia bulk

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

È possibile eseguire più operazioni di copia bulk usando una singola istanza di una classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy>. Se i parametri delle operazioni cambiano tra le copie (ad esempio, il nome della tabella di destinazione), è necessario aggiornarli prima delle chiamate successive a uno dei metodi **WriteToServer**, come illustrato nell'esempio seguente. A meno che non vengano modificati in modo esplicito, tutti i valori delle proprietà rimangono invariati rispetto alla precedente operazione di copia bulk per una determinata istanza.  
  
> [!NOTE]
>  L'esecuzione di più operazioni di copia bulk usando la stessa istanza di <xref:Microsoft.Data.SqlClient.SqlBulkCopy> in genere è più efficiente rispetto all'uso di un'istanza distinta per ogni operazione.  
  
Se si eseguono più operazioni di copia bulk usando lo stesso oggetto <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, non vi sono restrizioni relativamente al fatto che le informazioni di origine o di destinazione sono uguali o diverse in ogni operazione. È tuttavia necessario assicurarsi che le informazioni di associazione delle colonne siano impostate correttamente ogni volta che si esegue la scrittura nel server.  

## <a name="example"></a>Esempio

> [!IMPORTANT]
>  Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Installazione di esempio della copia bulk](bulk-copy-example-setup.md). Il codice viene fornito solo per illustrare la sintassi relativa all'uso di **SqlBulkCopy**. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL `INSERT … SELECT` per copiare i dati.  
  
[!code-csharp[DataWorks SqlBulkCopy_._ColumnMappingOrdersDetails#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnMappingOrdersDetails.cs#1)]
  
## <a name="next-steps"></a>Passaggi successivi
- [Operazioni di copia bulk in SQL Server](bulk-copy-operations-sql-server.md)
