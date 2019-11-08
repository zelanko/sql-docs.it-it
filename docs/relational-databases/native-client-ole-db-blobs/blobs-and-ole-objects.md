---
title: Oggetti BLOB e OLE | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b4e284d2086684af232c17b59675b834b26f497b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790634"
---
# <a name="blobs-and-ole-objects"></a>Oggetti BLOB e OLE
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client espone l'interfaccia **ISequentialStream** per supportare l'accesso del consumer a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**, **Text**, **Image**, **varchar (max)** , **nvarchar (max)** , **varbinary (max)** , e tipi di dati XML come oggetti binari di grandi dimensioni (BLOB). Il metodo **Read** in **ISequentialStream** consente al consumer di recuperare una quantità elevata di dati in blocchi gestibili.  
  
 Per un esempio che illustra questa funzionalità, vedere [impostare OLE DB&#41;di &#40;dati di grandi dimensioni](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md).  
  
 Il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB può utilizzare un'interfaccia **IStorage** implementata dal consumer quando il consumer fornisce il puntatore di interfaccia in una funzione di accesso associata per la modifica dei dati.  
  
 Per i tipi di dati con valori di grandi dimensioni, il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB controlla i presupposti per le dimensioni del tipo nelle interfacce **IRowset** e DDL. Le colonne con tipi di dati **varchar**, **nvarchar**e **varbinary** con dimensioni massime impostate su Unlimited verranno rappresentate come Long lungo i set di righe dello schema e le interfacce che restituiscono i tipi di dati della colonna.  
  
 Il provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client espone i tipi **varchar (max**), **varbinary (max)** e **nvarchar (max)** come DBTYPE_STR, DBTYPE_BYTES e DBTYPE_WSTR rispettivamente.  
  
 In un'applicazione è possibile utilizzare questi tipi nei modi seguenti:  
  
-   Eseguire l'associazione come tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Se le dimensioni de buffer non sono sufficienti, si verificherà il troncamento, esattamente come accade per questi tipi nelle release precedenti, anche se ora sono disponibili valori più grandi.  
  
-   Eseguire l'associazione come tipo e specificare DBTYPE_BYREF.  
  
-   Eseguire l'associazione come DBTYPE_IUNKNOWN e utilizzare il flusso.  
  
 Se si esegue l'associazione a DBTYPE_IUNKNOWN, viene utilizzata la funzionalità di flusso di ISequentialStream. Il provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supporta l'associazione di parametri di output come DBTYPE_IUNKNOWN per i tipi di dati con valori di grandi dimensioni per semplificare gli scenari in cui un stored procedure restituisce questi tipi di dati come valori restituiti che verranno esposti come DBTYPE_IUNKNOWN al client.  
  
## <a name="storage-object-limitations"></a>Limitazioni degli oggetti di archiviazione  
  
-   Il provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client può supportare solo un singolo oggetto di archiviazione aperto. I tentativi di aprire più di un oggetto di archiviazione (per ottenere un riferimento su più di un puntatore di interfaccia **ISequentialStream**) restituiscono DBSTATUS_E_CANTCREATE.  
  
-   Nel provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB, il valore predefinito della proprietà di sola lettura DBPROP_BLOCKINGSTORAGEOBJECTS è VARIANT_TRUE. Tale valore indica che se un oggetto di archiviazione è attivo, alcuni metodi (diversi da quelli degli oggetti di archiviazione) non riusciranno e verrà restituito E_UNEXPECTED.  
  
-   La lunghezza dei dati presentati da un oggetto di archiviazione implementato dal consumer deve essere nota al provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB quando viene creata la funzione di accesso Row che fa riferimento all'oggetto di archiviazione. Il consumer deve associare un indicatore di lunghezza nella struttura DBBINDING utilizzata per la creazione della funzione di accesso.  
  
-   Se una riga contiene più di un singolo valore di dati di grandi dimensioni e DBPROP_ACCESSORDER non è DBPROPVAL_AO_RANDOM, il consumer deve utilizzare un set di righe supportato dal cursore del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB per recuperare i dati di riga o elaborare tutti i valori di dati di grandi dimensioni prima di recupero di altri valori di riga. Se DBPROP_ACCESSORDER è DBPROPVAL_AO_RANDOM, il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client memorizza nella cache tutti i tipi di dati XML come oggetti binari di grandi dimensioni (BLOB), in modo che sia possibile accedervi in qualsiasi ordine.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Recupero di dati di grandi dimensioni](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [Impostazione di dati di grandi dimensioni](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [Supporto del flusso per parametri di output BLOB](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native client &#40;OLE DB&#41; ](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Uso di tipi valore di grandi dimensioni](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
