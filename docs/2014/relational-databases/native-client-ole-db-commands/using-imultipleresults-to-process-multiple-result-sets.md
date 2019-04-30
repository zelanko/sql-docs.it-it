---
title: Uso di IMultipleResults per elaborare più set di risultati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: e160733e01c3df2063a57d61bb8178438d383e1a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155020"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>Utilizzo dell'interfaccia IMultipleResults per elaborare più set di risultati
  I consumer utilizzano le **IMultipleResults** interface per elaborare i risultati restituiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esecuzione dei comandi del provider OLE DB Native Client. Quando la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client invia un comando per l'esecuzione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue le istruzioni e restituisce i risultati.  
  
 Tutti i risultati ottenuti dall'esecuzione dei comandi devono essere elaborati da un client. Poiché il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esecuzione dei comandi del provider OLE DB Native Client può generare oggetti più set di righe dei risultati, usare il **IMultipleResults** interfaccia per assicurare che il recupero dei dati dell'applicazione completi il andata inizializzata sul lato client.  
  
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
  
 Se un consumer esegue un comando contenente questo testo e richiede un set di righe come interfaccia dei risultati restituiti, viene restituito solo il primo set di righe. Il consumer può elaborare tutte le righe del set di righe restituito. Ma, se la proprietà dell'origine dati DBPROP_MULTIPLECONNECTIONS è impostata su VARIANT_FALSE e MARS non è abilitato per la connessione, nessun altro comando può essere eseguito sull'oggetto sessione (il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client non creerà un altro connessione) fino a quando non viene annullato. Se MARS non è abilitato per la connessione, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce un errore DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS è VARIANT_FALSE e restituisce E_FAIL se è presente una transazione attiva.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituirà anche DB_E_OBJECTOPEN quando si usa trasmettere i parametri di output e l'applicazione non ha utilizzato tutti i valori di parametro di output restituiti prima di chiamare **IMultipleResults:: GetResults**  per ottenere il set di risultati successivo. Se MARS non è abilitato e la connessione sta eseguendo un comando che non produce un set di righe o che produce un set di righe che non è un cursore del server e se la proprietà dell'origine dati DBPROP_MULTIPLECONNECTIONS è impostata su VARIANT_TRUE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Provider OLE DB consente di creare connessioni aggiuntive per supportare gli oggetti comando simultanei, a meno che una transazione è attiva, nel qual caso restituisce un errore. Le transazioni e il blocco vengono gestiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per singola connessione. Se viene generata una seconda connessione, il comando sulle connessioni separate non condivide i blocchi. È necessario assicurarsi che un comando non blocchi un altro comando mantenendo attivi i blocchi sulle righe richieste da quest'ultimo. Se MARS è abilitato, è possibile disporre di più comandi attivi sulle connessioni e se vengono utilizzate transazioni esplicite tutti i comandi condividono una transazione comune.  
  
 Il consumer può annullare il comando usando [ISSAbort::Abort](../native-client-ole-db-interfaces/issabort-abort-ole-db.md) oppure rilasciando tutti i riferimenti mantenuti sull'oggetto comando e sul set di righe derivato.  
  
 Se **IMultipleResults** viene usato in tutte le istanze, il consumer può ottenere tutti i set di righe generati dall'esecuzione dei comandi e determinare in modo appropriato il momento in cui annullare l'esecuzione dei comandi e liberare un oggetto sessione per consentirne l'uso da parte di altri comandi.  
  
> [!NOTE]  
>  Quando si utilizzano cursori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'esecuzione di comandi crea il cursore. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce l'esito positivo o negativo della creazione del cursore. Pertanto, il round trip all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene completato al momento della restituzione da parte dell'esecuzione di comandi. Ogni chiamata a **GetNextRows** diventa quindi un round trip. In questo modo, possono esistere più oggetti comando attivi, ognuno dei quali elabora un set di righe che rappresenta il risultato di un recupero dal cursore del server. Per altre informazioni, vedere [Set di righe e cursori SQL Server](../native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Comandi](commands.md)  
  
  
