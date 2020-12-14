---
title: Gestire eventi DataAdapter
description: Descrive gli eventi DataAdapter e come usarli.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 11515b25-ee49-4b1d-9294-a142147c1ec5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 003a8e77ad80f83c210ffb565ce4fac5c93c2166
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772220"
---
# <a name="handle-dataadapter-events"></a>Gestire eventi DataAdapter

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Il provider di dati Microsoft SqlClient per SQL Server <xref:Microsoft.Data.SqlClient.SqlDataAdapter> espone tre eventi che è possibile usare per rispondere alle modifiche apportate ai dati nell'origine dati. Nella tabella seguente vengono descritti gli eventi di `DataAdapter`.

|Event|Descrizione|  
|-----------|-----------------|  
|`RowUpdating`|Sta per iniziare un'operazione UPDATE, INSERT o DELETE su una riga tramite la chiamata a uno dei metodi `Update`.|  
|`RowUpdated`|È stata completata un'operazione UPDATE, INSERT o DELETE su una riga tramite la chiamata a uno dei metodi `Update`.|  
|`FillError`|Si è verificato un errore durante un'operazione `Fill`.|  

## <a name="rowupdating-and-rowupdated-events"></a>Eventi RowUpdating e RowUpdated

`RowUpdating` viene generato prima che un aggiornamento a una riga di <xref:System.Data.DataSet> sia stato elaborato nell'origine dati. `RowUpdated` viene generato dopo che un aggiornamento a una riga di `DataSet` è stato elaborato nell'origine dati. Di conseguenza, è possibile usare `RowUpdating` per modificare il comportamento dell'aggiornamento prima che venga eseguito, in modo da fornire una gestione aggiuntiva quando verrà eseguito l'aggiornamento, conservare un riferimento a una riga aggiornata, annullare l'aggiornamento corrente e pianificarlo per un processo in batch che verrà eseguito successivamente e così via. `RowUpdated` risulta utile per rispondere a errori ed eccezioni che si verificano durante l'aggiornamento. È possibile aggiungere a `DataSet` le **informazioni sull'errore**, ma anche la **logica di ripetizione dei tentativi** e così via.

Gli argomenti <xref:System.Data.Common.RowUpdatingEventArgs> e <xref:System.Data.Common.RowUpdatedEventArgs> passati agli eventi `RowUpdating` e `RowUpdated` includono una proprietà `Command` che fa riferimento all'oggetto `Command` usato per eseguire l'aggiornamento, una proprietà `Row` che fa riferimento all'oggetto `DataRow` contenente le informazioni aggiornate, una proprietà `StatementType` relativa al tipo di aggiornamento eseguito, l'oggetto `TableMapping`, se applicabile, e lo `Status` dell'operazione.

È possibile usare la proprietà `Status` per determinare se si è verificato un errore durante l'operazione ed eventualmente per controllare le operazioni relative alle righe correnti e risultanti. Quando si verifica l'evento, la proprietà `Status` sarà uguale a `Continue` o `ErrorsOccurred`. Nella tabella seguente sono indicati i valori su cui è possibile impostare la proprietà `Status` per controllare le operazioni successive durante l'aggiornamento.

|Stato|Descrizione|  
|------------|-----------------|  
|`Continue`|Continua l'operazione di aggiornamento.|  
|`ErrorsOccurred`|Interrompe l'operazione di aggiornamento e genera un'eccezione.|  
|`SkipCurrentRow`|Ignora la riga corrente e continua l'operazione di aggiornamento.|  
|`SkipAllRemainingRows`|Interrompe l'operazione di aggiornamento, ma non genera un'eccezione.|  

Se si imposta la proprietà `Status` su `ErrorsOccurred`, verrà generata un'eccezione. È possibile controllare l'eccezione generata impostando la proprietà `Errors` sull'eccezione desiderata. Se si usa uno degli altri valori di `Status` non verrà generata alcuna eccezione.

È inoltre possibile usare la proprietà `ContinueUpdateOnError` per gestire gli errori relativi alle righe aggiornate. Se `DataAdapter.ContinueUpdateOnError` è `true`, quando un aggiornamento di una riga determina la generazione di un'eccezione, il testo dell'eccezione viene inserito nelle informazioni `RowError` della stessa riga e l'elaborazione continua senza generare un'eccezione. In questo modo è possibile rispondere agli errori quando l'evento `Update` è completato, a differenza di quanto avviene con l'evento `RowUpdated` che consente di rispondere agli errori nel momento in cui si verificano.

Nell'esempio di codice seguente viene illustrato come aggiungere e rimuovere i gestori eventi. Il gestore dell'evento `RowUpdating` scrive un log di tutti i record eliminati con un timestamp. Il gestore dell'evento `RowUpdated` aggiunge le informazioni sugli errori alla proprietà `RowError` della riga in `DataSet`, evita la generazione dell'eccezione e continua l'elaborazione, riproducendo quindi il comportamento di `ContinueUpdateOnError` = `true`.

[!code-csharp[SqlDataAdapter_Events#1](~/../sqlclient/doc/samples/SqlDataAdapter_Events.cs#1)]

## <a name="fillerror-event"></a>FillError (evento)

`DataAdapter` genera l'evento `FillError` quando si verifica un errore durante un'operazione `Fill`. Questo tipo di errore si verifica in genere quando i dati nella riga da aggiungere non possono essere convertiti in un tipo .NET senza una perdita di precisione.

Se si verifica un errore durante un'operazione `Fill`, la riga corrente non verrà aggiunta a `DataTable`. L'evento `FillError` consente di risolvere l'errore e aggiungere la riga o di ignorare la riga esclusa e continuare l'operazione `Fill`.

<xref:System.Data.FillErrorEventArgs> passato all'evento `FillError` può contenere diverse proprietà che consentono di rispondere agli errori e di risolverli. Nella tabella seguente sono illustrate le proprietà dell'oggetto `FillErrorEventArgs`.

|Proprietà|Descrizione|  
|--------------|-----------------|  
|`Errors`|`Exception` generata.|  
|`DataTable`|Oggetto `DataTable` in fase di riempimento quando si è verificato l'errore.|  
|`Values`|Matrice di oggetti contenente i valori della riga in fase di inserimento quando si è verificato l'errore. I riferimenti ordinali della matrice di `Values` corrispondono ai riferimenti ordinali delle colonne della riga che viene aggiunta. `Values[0]`, ad esempio, è il valore che era stato aggiunto come prima colonna della riga.|  
|`Continue`|Consente di scegliere se generare o meno una Exception. Se si imposta la proprietà `Continue` su `false`, l'operazione `Fill` corrente verrà interrotta e verrà generata un'eccezione. Se si imposta `Continue` su `true`, l'operazione `Fill` continuerà nonostante l'errore.|  

Nell'esempio di codice seguente viene aggiunto un gestore per l'evento `FillError` di `DataAdapter`. Nel codice dell'evento `FillError` viene determinato se esiste il rischio potenziale di una perdita di precisione e viene fornita la possibilità di rispondere all'eccezione.

[!code-csharp[SqlDataAdapter_Events#2](~/../sqlclient/doc/samples/SqlDataAdapter_Events.cs#2)]

## <a name="see-also"></a>Vedere anche

- [DataAdapter e DataReader](dataadapters-datareaders.md)
- [Eventi](/dotnet/standard/events/index.md)
- [Microsoft ADO.NET per SQL Server](microsoft-ado-net-sql-server.md)
