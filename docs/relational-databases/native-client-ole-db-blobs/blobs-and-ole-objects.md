---
title: BLOB e oggetti OLE | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d0cb9751940489513f939ab8ee52728c6b75e925
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297689"
---
# <a name="blobs-and-ole-objects"></a>Oggetti BLOB e OLE
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client espone l'interfaccia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ISequentialStream** per supportare l'accesso dei consumer a tipi di dati **ntext**, **text**, **image**, **varchar(max)**, **nvarchar(max)** **varbinary(max)** e xml come oggetti binari di grandi dimensioni (BLOB). Il metodo **Read** in **ISequentialStream** consente al consumer di recuperare una quantità elevata di dati in blocchi gestibili.  
  
 Per un esempio che illustra questa funzionalità, vedere [Impostare dati di grandi dimensioni &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md).  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client può utilizzare un'interfaccia **IStorage** implementata dal consumatore quando il consumer fornisce il puntatore a interfaccia in una funzione di accesso associata per la modifica dei dati.  
  
 Per i tipi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati valore di grandi dimensioni, il provider OLE DB Native Client verifica i presupposti della dimensione dei tipi nelle interfacce **IRowset** e DDL. Le colonne con tipi di dati **varchar**, **nvarchar**e **varbinary** con dimensione massima impostata su unlimited verranno rappresentate come ISLONG tramite i set di righe dello schema e le interfacce che restituiscono tipi di dati di colonna.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client espone i tipi **varchar(max),** **varbinary(max)** e **nvarchar(max)** come DBTYPE_STR, DBTYPE_BYTES e DBTYPE_WSTR rispettivamente.  
  
 In un'applicazione è possibile utilizzare questi tipi nei modi seguenti:  
  
-   Eseguire l'associazione come tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Se le dimensioni de buffer non sono sufficienti, si verificherà il troncamento, esattamente come accade per questi tipi nelle release precedenti, anche se ora sono disponibili valori più grandi.  
  
-   Eseguire l'associazione come tipo e specificare DBTYPE_BYREF.  
  
-   Eseguire l'associazione come DBTYPE_IUNKNOWN e utilizzare il flusso.  
  
 Se si esegue l'associazione a DBTYPE_IUNKNOWN, viene utilizzata la funzionalità di flusso di ISequentialStream. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta i parametri di output di associazione come DBTYPE_IUNKNOWN per i tipi di dati valore di grandi dimensioni per facilitare gli scenari in cui una stored procedure restituisce questi tipi di dati come valori restituiti che verranno esposti come DBTYPE_IUNKNOWN al client.  
  
## <a name="storage-object-limitations"></a>Limitazioni degli oggetti di archiviazione  
  
-   Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client può supportare solo un singolo oggetto di archiviazione aperto. I tentativi di aprire più di un oggetto di archiviazione (per ottenere un riferimento su più di un puntatore di interfaccia **ISequentialStream**) restituiscono DBSTATUS_E_CANTCREATE.  
  
-   Nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client, il valore predefinito della proprietà DBPROP_BLOCKINGSTORAGEOBJECTS di sola lettura è VARIANT_TRUE. Tale valore indica che se un oggetto di archiviazione è attivo, alcuni metodi (diversi da quelli degli oggetti di archiviazione) non riusciranno e verrà restituito E_UNEXPECTED.  
  
-   La lunghezza dei dati presentati da un oggetto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archiviazione implementato dal consumer deve essere resa nota al provider OLE DB Native Client quando viene creata la funzione di accesso di riga che fa riferimento all'oggetto di archiviazione. Il consumer deve associare un indicatore di lunghezza nella struttura DBBINDING utilizzata per la creazione della funzione di accesso.  
  
-   Se una riga contiene più di un singolo valore di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grandi dimensioni e DBPROP_ACCESSORDER non è DBPROPVAL_AO_RANDOM, il consumer deve utilizzare un set di righe supportato dal cursore del provider OLE DB Native Client per recuperare i dati della riga o elaborare tutti i valori di dati di grandi dimensioni prima di recuperare altri valori di riga. Se DBPROP_ACCESSORDER è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROPVAL_AO_RANDOM, il provider OLE DB Native Client memorizza nella cache tutti i tipi di dati xml come oggetti binari di grandi dimensioni (BLOB) in modo che sia possibile accedervi in qualsiasi ordine.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Recupero di dati di grandi dimensioni](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [Impostazione di dati di grandi dimensioni](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [Supporto del flusso per parametri di output BLOB](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Vedere anche  
 [&#41;OLE DB &#40;SQL Server Native Client](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Utilizzo di tipi di dati per valori di grandi dimensioni](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
