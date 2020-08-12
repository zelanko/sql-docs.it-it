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
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 685bb349366ad955248a05e23ec030788dcbc63d
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2020
ms.locfileid: "85106912"
---
# <a name="transaction-and-bulk-copy-operations"></a>Transazioni e operazioni di copia bulk

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Le operazioni di copia bulk possono essere eseguite come operazioni isolate oppure come parte di una transazione in più passaggi. La seconda opzione consente di eseguire più di un'operazione di copia bulk all'interno della stessa transazione, nonché di eseguire altre operazioni sul database, tra cui inserimenti, aggiornamenti ed eliminazioni, mantenendo comunque la possibilità di eseguire il commit o il rollback dell'intera transazione.  
  
Per impostazione predefinita, un'operazione di copia bulk viene eseguita come operazione isolata. L'operazione di copia bulk avviene in modalità non transazionale, senza la possibilità di eseguirne il rollback. Se è necessario eseguire il roll back di tutta o parte della copia bulk quando si verifica un errore, è possibile:

 - Usare una transazione gestita da <xref:Microsoft.Data.SqlClient.SqlBulkCopy>

 - Eseguire l'operazione di copia bulk all'interno di una transazione esistente

 - Integrare l'operazione in un oggetto **System.Transactions** <xref:System.Transactions.Transaction>.  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>Esecuzione di un'operazione di copia bulk non transazionale  
L'applicazione console seguente illustra cosa accade quando si verifica un errore durante un'operazione di copia bulk non transazionale.  
  
Nell'esempio, le tabelle di origine e di destinazione contengono entrambe una colonna `Identity` denominata **ProductID**. Il codice innanzitutto prepara la tabella di destinazione eliminando tutte le righe e quindi inserendo una singola riga il cui **ProductID** è presente nella tabella di origine. Per impostazione predefinita, viene generato un nuovo valore per la colonna `Identity` nella tabella di destinazione per ogni riga aggiunta. In questo esempio, all'apertura della connessione viene impostata un'opzione che impone al processo di caricamento bulk di usare i valori `Identity` dalla tabella di origine.  
  
L'operazione di copia bulk viene eseguita con la proprietà <xref:Microsoft.Data.SqlClient.SqlBulkCopy.BatchSize%2A>impostata su 10. Quando l'operazione riscontra la riga non valida, viene generata un'eccezione. In questo primo esempio, l'operazione di copia bulk è non transazionale. Viene eseguito il commit di tutti i batch copiati fino al punto dell'errore. Viene eseguito il ripristino dello stato precedente del batch che contiene la chiave duplicata e l'operazione di copia bulk viene interrotta prima dell'elaborazione dei batch rimanenti.  
  
> [!NOTE]
>  Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Installazione di esempio della copia bulk](bulk-copy-example-setup.md). Il codice viene fornito solo per illustrare la sintassi relativa all'uso di **SqlBulkCopy**. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL `INSERT … SELECT` per copiare i dati.  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_Default#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_Default.cs#1)]
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>Esecuzione di un'operazione di copia bulk dedicata in una transazione  
Per impostazione predefinita, un'operazione di copia bulk costituisce la propria transazione. Quando si vuole eseguire un'operazione di copia bulk dedicata, creare un'istanza di <xref:Microsoft.Data.SqlClient.SqlBulkCopy> con una stringa di connessione oppure usare un oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> esistente senza una transazione attiva. L'operazione di copia bulk crea una transazione in ogni scenario e quindi ne esegue il commit o il ripristino dello stato precedente.  
  
È possibile specificare in modo esplicito l'opzione <xref:Microsoft.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> nel costruttore di classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> per eseguire un'operazione di copia bulk nella relativa transazione. Ogni batch dell'operazione viene eseguito all'interno di una transazione separata.  
  
> [!NOTE]
>  Poiché i diversi batch vengono eseguiti in diverse transazioni, se si verifica un errore durante l'operazione di copia bulk, verrà eseguito il rollback di tutte le righe nel batch corrente, ma le righe dei batch precedenti rimarranno nel database.  
  
L'applicazione console seguente è simile all'esempio precedente, con una sola eccezione: in questo esempio l'operazione di copia bulk gestisce le proprie transazioni. Viene eseguito il commit di tutti i batch copiati fino al punto dell'errore. Viene eseguito il ripristino dello stato precedente del batch che contiene la chiave duplicata e l'operazione di copia bulk viene interrotta prima dell'elaborazione dei batch rimanenti. 
  
> [!IMPORTANT]
>  Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Installazione di esempio della copia bulk](bulk-copy-example-setup.md). Il codice viene fornito solo per illustrare la sintassi relativa all'uso di **SqlBulkCopy**. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL `INSERT … SELECT` per copiare i dati.  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_UseInternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_UseInternalTransaction.cs#1)]
  
## <a name="using-existing-transactions"></a>Utilizzo di transazioni esistenti  
È possibile specificare un oggetto <xref:Microsoft.Data.SqlClient.SqlTransaction> esistente come parametro in un costruttore <xref:Microsoft.Data.SqlClient.SqlBulkCopy>. In questo caso, l'operazione di copia bulk viene eseguita in una transazione esistente e non viene apportata alcuna modifica allo stato della transazione, ovvero non viene eseguito il commit della transazione né questa viene interrotta. Questo metodo consente a un'applicazione di includere l'operazione di copia bulk in una transazione con altre operazioni sul database. Se tuttavia non si specifica un oggetto <xref:Microsoft.Data.SqlClient.SqlTransaction>, si passa un riferimento null e la connessione ha una transazione attiva, viene generata un'eccezione.   
  
Se è necessario eseguire il rollback dell'intera copia bulk perché si verifica un errore o se la copia bulk deve essere eseguita come parte di un processo più ampio di cui è possibile eseguire il rollback, è possibile aggiungere un oggetto <xref:Microsoft.Data.SqlClient.SqlTransaction> al costruttore <xref:Microsoft.Data.SqlClient.SqlBulkCopy>.  
  
L'applicazione console seguente è simile al primo esempio (non transazionale), con una sola eccezione: in questo esempio, l'operazione di copia bulk è inclusa in una transazione esterna di maggiori dimensioni. Quando si verifica l'errore di violazione della chiave primaria, viene eseguito il rollback dell'intera transazione e non vengono aggiunte righe alla tabella di destinazione.  
  
> [!IMPORTANT]
>  Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Installazione di esempio della copia bulk](bulk-copy-example-setup.md). Il codice viene fornito solo per illustrare la sintassi relativa all'uso di **SqlBulkCopy**. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL `INSERT … SELECT` per copiare i dati.  
  
[!code-csharp[DataWorks SqlBulkCopy_ExternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopy_ExternalTransaction.cs#1)]
  
## <a name="next-steps"></a>Passaggi successivi
- [Operazioni di copia bulk in SQL Server](bulk-copy-operations-sql-server.md)
