---
title: Elaborazione dei risultati (OLE DB Driver)
description: Informazioni sul modo in cui il consumer di OLE DB Driver per SQL Server ottiene e accede ai dati di un set di righe prodotto da un comando o generato da un provider.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [OLE DB Driver for SQL Server]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3cea6c2ef9cfdab250966cbd809be44e6506e4dc
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861537"
---
# <a name="processing-results"></a>Risultati dell'elaborazione
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Se un oggetto set di righe viene prodotto dall'esecuzione di un comando o dalla generazione di un oggetto set di righe direttamente dal provider, il consumer deve recuperare e accedere ai dati nel set di righe.  
  
 I set di righe sono gli oggetti centrali che consentono a OLE DB Driver per SQL Server di esporre i dati in formato tabulare. Concettualmente, un set di righe è un set in cui ogni riga include dati di colonne Un oggetto set di righe espone interfacce come **IRowset**, che contiene metodi per il recupero di righe in sequenza dal set di righe, **IAccessor**, che permette la definizione di un gruppo di associazioni di colonna che descrivono la modalità di associazione dei dati tabulari alle variabili del programma di tipo consumer, **IColumnsInfo**, che fornisce informazioni sulle colonne nel set di righe, e **IRowsetInfo**, che fornisce informazioni sul set di righe.  
  
 Un utente può chiamare il metodo **IRowset::GetData** per recuperare una riga di dati dal set di righe in un buffer. Prima che venga chiamato **GetData**, il consumer descrive il buffer mediante un set di strutture DBBINDING. Ogni associazione descrive la modalità di archiviazione di una colonna in un set di righe in un buffer del consumer e contiene gli elementi seguenti:  
  
-   Ordinale della colonna, o parametro, a cui si applica l'associazione.  
  
-   Informazioni sugli elementi associati, ad esempio, valore dei dati, lunghezza dei dati e relativo stato dell'associazione.  
  
-   Informazioni sugli offset presenti nel buffer per ciascuna di queste parti.  
  
-   Lunghezza e tipo dei valori dei dati inclusi nel buffer del consumer.  
  
 Quando si recuperano i dati, il provider utilizza le informazioni presenti in ogni associazione per determinare dove e come recuperare i dati dal buffer del consumer. Durante l'impostazione dei dati nel buffer del consumer, il provider utilizza le informazioni presenti in ogni associazione per determinare dove e come restituire i dati all'interno del buffer.  
  
 Dopo aver specificato le strutture DBBINDING, viene creata una funzione di accesso (**IAccessor::CreateAccessor**). Una funzione di accesso è una raccolta di associazioni e viene utilizzata per ottenere o impostare i dati nel buffer del consumer.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un driver OLE DB per applicazione SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [Procedure relative a OLE DB](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
