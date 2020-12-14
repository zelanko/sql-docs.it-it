---
title: Operazioni batch tramite DataAdapter
description: Descrive come migliorare le prestazioni dell'applicazione riducendo il numero di round trip a SQL Server quando si applicano gli aggiornamenti da DataSet.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: e72ed5af-b24f-486c-8429-c8fd2208f844
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 1b720dff0678c68396fe7d8cf1f60f3ade70dd9d
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772265"
---
# <a name="batch-operations-using-dataadapters"></a>Operazioni batch tramite DataAdapter

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Il supporto batch in ADO.NET consente a un tipo <xref:System.Data.Common.DataAdapter> di raggruppare le operazioni INSERT, UPDATE e DELETE da un tipo <xref:System.Data.DataSet> o <xref:System.Data.DataTable> e di inviarle al server in batch, anziché inviare una singola operazione alla volta. La riduzione nel numero di percorsi di andata e ritorno al server determina in genere un notevole miglioramento delle prestazioni. L'aggiornamento batch è supportato per il provider di dati Microsoft SqlClient per SQL Server (<xref:Microsoft.Data.SqlClient>).

Per l'aggiornamento di un database con modifiche provenienti da un <xref:System.Data.DataSet>, nelle versioni precedenti di ADO.NET il metodo `Update` di un `DataAdapter` eseguiva gli aggiornamenti del database una riga alla volta. Scorrendo le righe nella <xref:System.Data.DataTable> specificata, ciascuna riga <xref:System.Data.DataRow> veniva esaminata per rilevare eventuali modifiche. Se la riga era stata modificata, veniva chiamato il comando appropriato `UpdateCommand`, `InsertCommand` o `DeleteCommand`, in base al valore della proprietà <xref:System.Data.DataRow.RowState%2A> per quella determinata riga. Ogni aggiornamento di riga comportava un percorso di andata e ritorno in rete al database.

Nel provider di dati Microsoft SqlClient per SQL Server, <xref:Microsoft.Data.SqlClient.SqlDataAdapter> espone una proprietà <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateBatchSize%2A>. Impostando `UpdateBatchSize` su un valore intero positivo, gli aggiornamenti vengono inviati al database come batch della dimensione specificata. Ad esempio, impostando `UpdateBatchSize` su 10, verranno raggruppate 10 istruzioni separate e inviate come singolo batch. Impostando `UpdateBatchSize` su 0, il <xref:Microsoft.Data.SqlClient.SqlDataAdapter> utilizzerà la dimensione di batch massima che il server è in grado di gestire. Se invece si imposta il valore su 1, gli aggiornamenti batch vengono disabilitati, in quanto le righe vengono inviate una alla volta.

> [!NOTE]
> Le prestazioni risulteranno ridotte se si esegue un batch di dimensioni molto elevate. Pertanto, prima di implementare l'applicazione è consigliabile verificare quale sia la dimensione ottimale per i batch.

## <a name="use-the-updatebatchsize-property"></a>Usare la proprietà UpdateBatchSize

Quando gli aggiornamenti batch sono abilitati, il valore della proprietà <xref:System.Data.IDbCommand.UpdatedRowSource%2A> dei comandi `UpdateCommand`, `InsertCommand` e `DeleteCommand` di Data Adapter deve essere impostato su <xref:System.Data.UpdateRowSource.None> o su <xref:System.Data.UpdateRowSource.OutputParameters>. Quando si esegue un aggiornamento batch, il valore <xref:System.Data.IDbCommand.UpdatedRowSource%2A> o <xref:System.Data.UpdateRowSource.FirstReturnedRecord> della proprietà <xref:System.Data.UpdateRowSource.Both> del comando non è valido.
  
Nella procedura seguente viene illustrato l'uso della proprietà `UpdateBatchSize`. La procedura accetta due argomenti, un oggetto <xref:System.Data.DataSet> contenente colonne che rappresentano i campi **ProductCategoryID** e **Name** della tabella **Production.ProductCategory** e un numero intero che rappresenta la dimensione del batch (il numero di righe nel batch). Il codice crea un nuovo oggetto <xref:Microsoft.Data.SqlClient.SqlDataAdapter>, impostandone le proprietà <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A>, <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> e <xref:Microsoft.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A>. Nel codice si presuppone che l'oggetto <xref:System.Data.DataSet> contenga righe modificate. La proprietà `UpdateBatchSize` viene impostata e viene eseguito l'aggiornamento.

[!code-csharp[SqlDataAdapter_Batch#1](~/../sqlclient/doc/samples/SqlDataAdapter_Batch.cs#1)]

## <a name="handle-batch-update-related-events-and-errors"></a>Gestire gli errori e gli eventi correlati all'aggiornamento batch

L'oggetto **DataAdapter** contiene due eventi correlati all'aggiornamento: **RowUpdating** e **RowUpdated**. Per altre informazioni, vedere [Gestire eventi DataAdapter](handle-dataadapter-events.md).

### <a name="event-behavior-changes-with-batch-updates"></a>Modifiche funzionali dell'evento con gli aggiornamenti batch

Quando l'elaborazione batch è abilitata, in un'unica operazione di database vengono aggiornate più righe. Pertanto, si verifica un solo evento `RowUpdated` per ogni batch, mentre l'evento `RowUpdating` si verifica per ogni riga elaborata. Quando l'elaborazione batch è disabilitata, i due eventi vengono generati con interfoliazione uno-a-uno, dove un evento `RowUpdating` e un evento `RowUpdated` vengono generati per una riga e un evento `RowUpdating` e un evento `RowUpdated` per la riga successiva, fino all'elaborazione di tutte le righe.

### <a name="access-updated-rows"></a>Accedere alle righe aggiornate

Quando l'elaborazione batch è disabilitata, è possibile accedere alla riga aggiornata mediante la proprietà <xref:System.Data.Common.RowUpdatedEventArgs.Row%2A> della classe <xref:System.Data.Common.RowUpdatedEventArgs>.

Quando l'elaborazione batch è abilitata, viene generato un unico evento `RowUpdated` per più righe. Pertanto, il valore della proprietà `Row` per ciascuna riga è null. Gli eventi `RowUpdating` vengono comunque generati per ogni riga. Il metodo <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A> della classe <xref:System.Data.Common.RowUpdatedEventArgs> consente di accedere alle righe elaborate mediante la copia dei riferimenti alle righe in una matrice. Se non viene elaborata nessuna riga, `CopyToRows` genera un'eccezione <xref:System.ArgumentNullException>. Usare la proprietà <xref:System.Data.Common.RowUpdatedEventArgs.RowCount%2A> per restituire il numero di righe elaborate prima di chiamare il metodo <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A>.

### <a name="handle-data-errors"></a>Gestire gli errori relativi ai dati

I risultati dell'esecuzione batch sono identici a quelli ottenuti eseguendo le singole istruzioni una alla volta. Le istruzioni vengono eseguite nell'ordine in base al quale sono state aggiunte al batch. La gestione degli errori è la stessa sia in modalità batch sia quando la modalità batch è disabilitata. Ogni riga viene elaborata separatamente. Solo le righe che sono state elaborate correttamente nel database verranno aggiornate nell'oggetto <xref:System.Data.DataRow> corrispondente all'interno di <xref:System.Data.DataTable>.

> [!NOTE]
> Il provider di dati Microsoft SqlClient per SQL Server e il server di database back-end determinano quali costrutti SQL sono supportati per l'esecuzione batch. Se per l'esecuzione viene inviata un'istruzione non supportata, è possibile che venga generata un'eccezione.

## <a name="see-also"></a>Vedere anche

- [DataAdapter e DataReader](dataadapters-datareaders.md)
- [Aggiornare origini dati con DataAdapter](update-data-sources-with-dataadapters.md)
- [Gestire eventi DataAdapter](handle-dataadapter-events.md)
- [Microsoft ADO.NET per SQL Server](microsoft-ado-net-sql-server.md)
