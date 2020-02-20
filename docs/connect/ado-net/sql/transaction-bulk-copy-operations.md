---
title: Transazioni e operazioni di copia bulk
description: Viene descritto come eseguire un'operazione di copia bulk all'interno di una transazione e come eseguire il commit o il ripristino dello stato precedente della transazione.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 465870aa05b97b841a23c0ca1843e3de395a0b8b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75233803"
---
# <a name="transaction-and-bulk-copy-operations"></a>Transazioni e operazioni di copia bulk

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Le operazioni di copia bulk possono essere eseguite come operazioni isolate oppure come parte di una transazione in più passaggi. Quest'ultima opzione consente di eseguire più di un'operazione di copia bulk all'interno della stessa transazione, nonché di eseguire altre operazioni sul database (come inserimenti, aggiornamenti ed eliminazioni), mantenendo comunque la possibilità di eseguire il commit o il rollback dell'intera transazione.  
  
Per impostazione predefinita, una copia bulk viene eseguita come un'operazione isolata. L'operazione di copia bulk avviene in modalità non transazionale, senza la possibilità di eseguirne il rollback. Se è necessario eseguire il rollback della copia bulk, interamente o in parte, quando si verifica un errore, è possibile usare una transazione gestita da <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, eseguire l'operazione di copia bulk all'interno di una transazione esistente oppure inserirla in **System.Transactions**<xref:System.Transactions.Transaction>.  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>Esecuzione di un'operazione di copia bulk non transazionale  
L'applicazione console seguente illustra cosa accade quando si verifica un errore durante un'operazione di copia bulk non transazionale.  
  
Nell'esempio, le tabelle di origine e di destinazione contengono entrambe una colonna `Identity` denominata **ProductID**. Il codice innanzitutto prepara la tabella di destinazione eliminando tutte le righe e quindi inserendo una singola riga il cui **ProductID** è presente nella tabella di origine. Per impostazione predefinita, viene generato un nuovo valore per la colonna `Identity` nella tabella di destinazione per ogni riga aggiunta. In questo esempio, all'apertura della connessione viene impostata un'opzione che impone al processo di caricamento bulk di usare i valori `Identity` dalla tabella di origine.  
  
L'operazione di copia bulk viene eseguita con la proprietà <xref:Microsoft.Data.SqlClient.SqlBulkCopy.BatchSize%2A>impostata su 10. Quando è rilevata la riga non valida, viene generata un'eccezione. In questo primo esempio, l'operazione di copia bulk è non transazionale. Viene eseguito il commit di tutti i batch copiati fino al punto dell'errore. Viene eseguito il rollback del batch che contiene la chiave duplicata e l'operazione di copia bulk viene interrotta prima dell'elaborazione di altri batch.  
  
> [!NOTE]
>  Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Installazione di esempio della copia bulk](bulk-copy-example-setup.md). Il codice viene fornito solo per illustrare la sintassi relativa all'uso di **SqlBulkCopy**. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL `INSERT … SELECT` per copiare i dati.  
  
[!code-csharp[DataWorks SqlBulkCopyOpeions_Default#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_Default.cs#1)]
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>Esecuzione di un'operazione di copia bulk dedicata in una transazione  
Per impostazione predefinita, un'operazione di copia bulk costituisce la propria transazione. Quando si vuole eseguire un'operazione di copia bulk dedicata, creare una nuova istanza di <xref:Microsoft.Data.SqlClient.SqlBulkCopy> con una stringa di connessione oppure usare un oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> esistente senza una transazione attiva. In questo scenario, l'operazione di copia bulk crea e quindi esegue il commit o il rollback della transazione.  
  
È possibile specificare esplicitamente l'opzione <xref:Microsoft.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> nel costruttore della classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> per fare in modo che un'operazione di copia bulk venga eseguita nella propria transazione, determinando l'esecuzione di ogni batch dell'operazione di copia bulk all'interno di una transazione distinta.  
  
> [!NOTE]
>  Poiché i diversi batch vengono eseguiti in diverse transazioni, se si verifica un errore durante l'operazione di copia bulk, verrà eseguito il rollback di tutte le righe nel batch corrente, ma le righe dei batch precedenti rimarranno nel database.  
  
L' applicazione console seguente è analoga all'esempio precedente, con una sola eccezione: In questo esempio l'operazione di copia bulk gestisce le proprie transazioni. Viene eseguito il commit di tutti i batch copiati fino al punto dell'errore. Viene eseguito il rollback del batch che contiene la chiave duplicata e l'operazione di copia bulk viene interrotta prima dell'elaborazione di altri batch.  
  
> [!IMPORTANT]
>  Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Installazione di esempio della copia bulk](bulk-copy-example-setup.md). Il codice viene fornito solo per illustrare la sintassi relativa all'uso di **SqlBulkCopy**. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL `INSERT … SELECT` per copiare i dati.  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_UseInternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_UseInternalTransaction.cs#1)]
  
## <a name="using-existing-transactions"></a>Utilizzo di transazioni esistenti  
È possibile specificare un oggetto <xref:Microsoft.Data.SqlClient.SqlTransaction> esistente come parametro in un costruttore <xref:Microsoft.Data.SqlClient.SqlBulkCopy>. In questo caso, l'operazione di copia bulk viene eseguita in una transazione esistente e non viene apportata alcuna modifica allo stato della transazione (ovvero, non ne viene eseguito il commit, né viene interrotta). Questo consente a un'applicazione di includere l'operazione di copia bulk in una transazione con altre operazioni sul database. Se tuttavia non si specifica un oggetto <xref:Microsoft.Data.SqlClient.SqlTransaction>, si passa un riferimento null e la connessione ha una transazione attiva, viene generata un'eccezione.  
  
Se è necessario eseguire il rollback dell'intera copia bulk perché si verifica un errore o se la copia bulk deve essere eseguita come parte di un processo più ampio di cui è possibile eseguire il rollback, è possibile aggiungere un oggetto <xref:Microsoft.Data.SqlClient.SqlTransaction> al costruttore <xref:Microsoft.Data.SqlClient.SqlBulkCopy>.  
  
L'applicazione console seguente è simile al primo esempio (non transazionale), con una sola eccezione: in questo esempio, l'operazione di copia bulk è inclusa in una transazione esterna di maggiori dimensioni. Quando si verifica l'errore di violazione della chiave primaria, viene eseguito il rollback dell'intera transazione e non vengono aggiunte righe alla tabella di destinazione.  
  
> [!IMPORTANT]
>  Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Installazione di esempio della copia bulk](bulk-copy-example-setup.md). Il codice viene fornito solo per illustrare la sintassi relativa all'uso di **SqlBulkCopy**. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL `INSERT … SELECT` per copiare i dati.  
  
[!code-csharp[DataWorks SqlBulkCopy_ExternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopy_ExternalTransaction.cs#1)]
  
## <a name="next-steps"></a>Passaggi successivi
- [Operazioni di copia bulk in SQL Server](bulk-copy-operations-sql-server.md)
