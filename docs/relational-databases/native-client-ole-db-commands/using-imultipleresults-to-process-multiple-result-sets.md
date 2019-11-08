---
title: Uso di IMultipleResults per elaborare più set di risultati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
ms.assetid: 754d3f30-7d94-4b67-8dac-baf2699ce9c6
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 52bf85ba17630cc9bd76865e759a55d9c4864afc
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73758225"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Utilizzo dell'interfaccia IMultipleResults per elaborare più set di risultati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  I consumer utilizzano l'interfaccia **IMultipleResults** per elaborare i risultati restituiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client OLE DB esecuzione del comando del provider. Quando il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client invia un comando per l'esecuzione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue le istruzioni e restituisce tutti i risultati.  
  
 Tutti i risultati ottenuti dall'esecuzione dei comandi devono essere elaborati da un client. Poiché l'esecuzione del comando del provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client può generare oggetti di più set di righe come risultati, utilizzare l'interfaccia **IMultipleResults** per garantire che il recupero dei dati dell'applicazione completi il round trip avviato dal client.  
  
 L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente genera più set di righe, alcuni dei quali contengono dati di riga della tabella **OrderDetails**, mentre altri contengono i risultati della clausola COMPUTE BY:  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 Se un consumer esegue un comando contenente questo testo e richiede un set di righe come interfaccia dei risultati restituiti, viene restituito solo il primo set di righe. Il consumer può elaborare tutte le righe del set di righe restituito. Tuttavia, se la proprietà DBPROP_MULTIPLECONNECTIONS origine dati è impostata su VARIANT_FALSE e MARS non è abilitato sulla connessione, non è possibile eseguire altri comandi sull'oggetto sessione (il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client non creerà un'altra connessione) fino a quando il comando non viene annullato. Se MARS non è abilitato sulla connessione, il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client restituisce un errore DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS è VARIANT_FALSE e restituisce E_FAIL se è presente una transazione attiva.  
  
 Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client restituirà anche DB_E_OBJECTOPEN quando si usano i parametri di output trasmessi e l'applicazione non ha utilizzato tutti i valori dei parametri di output restituiti prima di chiamare **IMultipleResults:: GetResults** per ottenere set di risultati successivo. Se MARS non è abilitato e la connessione è occupata eseguendo un comando che non produce un set di righe o che produce un set di righe che non è un cursore del server e la proprietà DBPROP_MULTIPLECONNECTIONS origine dati è impostata su VARIANT_TRUE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB il provider crea connessioni aggiuntive per supportare gli oggetti comando simultanei, a meno che non sia attiva una transazione, nel qual caso viene restituito un errore. Le transazioni e il blocco vengono gestiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per singola connessione. Se viene generata una seconda connessione, il comando sulle connessioni separate non condivide i blocchi. È necessario assicurarsi che un comando non blocchi un altro comando mantenendo attivi i blocchi sulle righe richieste da quest'ultimo. Se MARS è abilitato, è possibile disporre di più comandi attivi sulle connessioni e se vengono utilizzate transazioni esplicite tutti i comandi condividono una transazione comune.  
  
 Il consumer può annullare il comando usando [ISSAbort::Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) oppure rilasciando tutti i riferimenti mantenuti sull'oggetto comando e sul set di righe derivato.  
  
 Se **IMultipleResults** viene usato in tutte le istanze, il consumer può ottenere tutti i set di righe generati dall'esecuzione dei comandi e determinare in modo appropriato il momento in cui annullare l'esecuzione dei comandi e liberare un oggetto sessione per consentirne l'uso da parte di altri comandi.  
  
> [!NOTE]  
>  Quando si utilizzano cursori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'esecuzione di comandi crea il cursore. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce l'esito positivo o negativo della creazione del cursore. Pertanto, il round trip all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene completato al momento della restituzione da parte dell'esecuzione di comandi. Ogni chiamata a **GetNextRows** diventa quindi un round trip. In questo modo, possono esistere più oggetti comando attivi, ognuno dei quali elabora un set di righe che rappresenta il risultato di un recupero dal cursore del server. Per altre informazioni, vedere [Set di righe e cursori SQL Server](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Comandi](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
