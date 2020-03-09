---
title: Singole operazioni di copia bulk
description: Viene descritto come eseguire una singola copia bulk dei dati in un'istanza di SQL Server usando la classe SqlBulkCopy e come eseguire l'operazione di copia bulk usando istruzioni Transact-SQL e la classe SqlCommand.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5e7ff0be-3f23-4996-a92c-bd54d65c3836
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 1029d9a0121b23963ccfc12582bd9d9cc7fd6cd6
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896595"
---
# <a name="single-bulk-copy-operations"></a>Singole operazioni di copia bulk

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

L'approccio più semplice per eseguire un'operazione di copia bulk di SQL Server consiste nell'eseguire una singola operazione su un database. Per impostazione predefinita, una copia bulk viene eseguita come un'operazione isolata: l'operazione di copia avviene in modalità non transazionale, senza la possibilità di eseguirne il rollback.  
  
> [!NOTE]
>  Se è necessario eseguire il rollback di una parte o dell'intera operazione di copia bulk quando si verifica un errore, è possibile usare una transazione gestita da <xref:Microsoft.Data.SqlClient.SqlBulkCopy> o eseguire l'operazione di copia bulk all'interno di una transazione esistente. **SqlBulkCopy** funzionerà anche con <xref:System.Transactions> se la connessione è inserita, in modo implicito o esplicito, in una transazione **System.Transactions**.  
>   
>  Per altre informazioni, vedere [Transazioni e operazioni di copia bulk](transaction-bulk-copy-operations.md).  
  
I passaggi generali per l'esecuzione di un'operazione di copia bulk sono i seguenti:  
  
1. Connettersi al server di origine e ottenere i dati da copiare. I dati possono provenire anche da altre origini, se possono essere recuperati da un oggetto <xref:System.Data.IDataReader> o <xref:System.Data.DataTable>.  
  
2. Connettersi al server di destinazione (la connessione può essere eseguita automaticamente anche da **SqlBulkCopy**).  
  
3. Creare un oggetto <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, impostando le eventuali proprietà necessarie.  
  
4. Impostare la proprietà **DestinationTableName** per indicare la tabella di destinazione per l'operazione di inserimento bulk.  
  
5. Chiamare uno dei metodi **WriteToServer**.  
  
6. Facoltativamente, aggiornare le proprietà e, se necessario, chiamare nuovamente **WriteToServer**.  
  
7. Chiamare <xref:Microsoft.Data.SqlClient.SqlBulkCopy.Close%2A> o eseguire il wrapping delle operazioni di copia bulk all'interno di un'istruzione `Using`.  
  
> [!CAUTION]
>  È consigliabile che i tipi di dati delle colonne di origine e di destinazione corrispondano. Se i tipi di dati non corrispondono, **SqlBulkCopy** tenterà di convertire ogni valore di origine nel tipo di dati di destinazione usando le regole impiegate da <xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>. Le conversioni possono influire sulle prestazioni, nonché provocare errori imprevisti. Ad esempio, un tipo di dati `Double` può essere convertito in un tipo di dati `Decimal` nella maggior parte dei casi, ma non sempre.  
  
## <a name="example"></a>Esempio  
L'applicazione console riportata di seguito dimostra come caricare i dati usando la classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy>. In questo esempio, viene usato un oggetto <xref:Microsoft.Data.SqlClient.SqlDataReader> per copiare i dati dalla tabella **Production.Product** del database **AdventureWorks** di SQL Server in una tabella simile dello stesso database.  
  
> [!IMPORTANT]
>  Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Installazione di esempio della copia bulk](bulk-copy-example-setup.md). Il codice viene fornito solo per illustrare la sintassi relativa all'uso di **SqlBulkCopy**. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL `INSERT … SELECT` per copiare i dati.  
  
[!code-csharp[DataWorks SqlBulkCopy_WriteToServer#1](~/../sqlclient/doc/samples/SqlBulkCopy_WriteToServer.cs#1)]
  
## <a name="performing-a-bulk-copy-operation-using-transact-sql-and-the-command-class"></a>Esecuzione di un'operazione di copia bulk usando Transact-SQL e la classe command  
Nell'esempio seguente viene illustrato come usare il metodo <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> per eseguire l'istruzione BULK INSERT.  
  
> [!NOTE]
>  Il percorso del file per l'origine dati è relativo al server. Affinché l'operazione di copia bulk abbia esito positivo, il processo server deve avere accesso a tale percorso.  
  
```csharp  
using (SqlConnection connection = New SqlConnection(connectionString))  
{  
string queryString =  "BULK INSERT Northwind.dbo.[Order Details] " +  
    "FROM 'f:\mydata\data.tbl' " +  
    "WITH ( FORMATFILE='f:\mydata\data.fmt' )";  
connection.Open();  
SqlCommand command = new SqlCommand(queryString, connection);  
  
command.ExecuteNonQuery();  
}  
```  
  
## <a name="next-steps"></a>Passaggi successivi
- [Operazioni di copia bulk in SQL Server](bulk-copy-operations-sql-server.md)
