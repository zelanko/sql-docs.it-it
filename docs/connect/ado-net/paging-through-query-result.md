---
title: Paging di un risultato di query
description: Viene fornito un esempio di visualizzazione dei risultati di una query sotto forma di pagine di dati.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: fa360c46-e5f8-411e-a711-46997771133d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 2de305e1069964f2d1a67b7f201578c7448d3e09
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772217"
---
# <a name="paging-through-a-query-result"></a>Paging di un risultato di query

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Il paging del risultato di una query corrisponde al processo di restituzione dei risultati di una query in subset di dati di dimensioni inferiori o pagine. Si tratta di una tecnica comunemente usata per la visualizzazione di risultati in blocchi di dimensioni ridotte e di facile gestione.

In <xref:Microsoft.Data.SqlClient.SqlDataAdapter> è disponibile una funzionalità che consente la restituzione di un'unica pagina di dati, tramite gli overload del metodo <xref:System.Data.Common.DbDataAdapter.Fill%2A>. Questa soluzione potrebbe non rivelarsi ottimale per il paging di una quantità elevata di risultati di query, perché, anche se **DataAdapter** compila la classe <xref:System.Data.DataTable> o <xref:System.Data.DataSet> di destinazione usando solo i record richiesti, le risorse per la restituzione dell'intera query sono ancora in uso.

Per restituire una pagina di dati da un'origine dati senza usare le risorse per la restituzione dell'intera query, specificare dei criteri aggiuntivi per la query, in modo che vengano restituite solo le righe necessarie.

Per usare il metodo <xref:System.Data.Common.DbDataAdapter.Fill%2A> per la restituzione di una pagina di dati, specificare un parametro **startRecord**, indicando il primo record della pagina di dati, e un parametro **maxRecords**, per il numero di record che devono essere contenuti nella pagina di dati.

## <a name="example"></a>Esempio

L'esempio di codice seguente mostra come usare il metodo <xref:System.Data.Common.DbDataAdapter.Fill%2A> per restituire la prima pagina di un risultato di una query, in cui la dimensione della pagina corrisponde a cinque record.

[!code-csharp[SqlDataAdapter_Paging#1](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#1)]

Nell'esempio precedente la classe **DataSet** viene compilata solo con cinque record, ma viene restituita l'intera tabella **Orders**. Per compilare la classe **DataSet** con gli stessi cinque record, ma restituire solo cinque record, usare le clausole `TOP` e `WHERE` nell'istruzione SQL, come illustrato nell'esempio seguente.

[!code-csharp[SqlDataAdapter_Paging#2](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#2)]

> [!NOTE]
> Quando si esegue il paging dei risultati della query in questo modo, è necessario mantenere l'elemento `unique identifier` che ordina le righe, per passare l'ID univoco al comando in modo da restituire la pagina successiva di record, come illustrato nell'esempio di codice seguente.

[!code-csharp[SqlDataAdapter_Paging#4](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#4)]

Per restituire l'elemento `next page of records` usando l'overload del metodo **Fill** che accetta i parametri **startRecord** e **maxRecords**, incrementare l'indice di record corrente sulla base della dimensione della pagina e compilare la tabella.

> [!NOTE]
> Ricordare che il server di database restituisce tutti i risultati della query, anche se a **DataSet** viene aggiunta solo una pagina di record.

Nell'esempio di codice seguente i contenuti delle tabelle vengono cancellati prima che tali tabelle siano compilate con la pagina successiva di dati. Per ridurre i percorsi al server database, è possibile archiviare in una cache locale un determinato numero di righe restituite.

[!code-csharp[SqlDataAdapter_Paging#3](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#3)]

Per restituire la pagina successiva di record senza che il server database restituisca l'intera query, specificare dei criteri restrittivi per l'istruzione SELECT. Poiché nell'esempio precedente l'ultimo record restituito viene conservato, è possibile usare tale record nella clausola WHERE per specificare un punto di partenza per la query, come illustrato nel seguente esempio di codice.

[!code-csharp[SqlDataAdapter_Paging#5](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#5)]

## <a name="see-also"></a>Vedere anche

- [DataAdapter e DataReader](dataadapters-datareaders.md)
- [Microsoft ADO.NET per SQL Server](microsoft-ado-net-sql-server.md)
