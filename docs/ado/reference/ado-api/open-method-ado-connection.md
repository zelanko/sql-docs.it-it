---
title: Metodo Open (connessione ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15115313613ea8f86dd2267c6be3c231cab92503
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931936"
---
# <a name="open-method-ado-connection"></a>Metodo Open (Connection - ADO)
Apre una connessione a un'origine dati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 Facoltativa. Valore **stringa** che contiene le informazioni di connessione. Per informazioni dettagliate sulle impostazioni valide, vedere la proprietà [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) .  
  
 *UserID*  
 Facoltativa. Valore **stringa** che contiene un nome utente da utilizzare per stabilire la connessione.  
  
 *Password*  
 Facoltativa. Valore **stringa** che contiene una password da utilizzare per stabilire la connessione.  
  
 *Opzioni*  
 Facoltativa. Valore [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) che determina se il metodo deve restituire dopo (in modo sincrono) o prima (in modo asincrono) che la connessione viene stabilita.  
  
## <a name="remarks"></a>Osservazioni  
 L'utilizzo del metodo **Open** su un oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) stabilisce la connessione fisica a un'origine dati. Una volta completato correttamente questo metodo, la connessione è attiva ed è possibile eseguire comandi su di essa ed elaborare i risultati.  
  
 Usare l'argomento facoltativo *ConnectionString* per specificare una stringa di connessione contenente una serie di istruzioni *argument* *= value* separate da punti e virgola o una risorsa di file o directory identificata con un URL. La proprietà **ConnectionString** eredita automaticamente il valore usato per l'argomento *ConnectionString* . Pertanto, è possibile impostare la proprietà **ConnectionString** dell'oggetto **Connection** prima di aprirla oppure utilizzare l'argomento *ConnectionString* per impostare o eseguire l'override dei parametri di connessione correnti durante la chiamata al metodo **Open** .  
  
 Se si passano informazioni sull'utente e sulla password sia nell'argomento *ConnectionString* che negli argomenti facoltativi *userid* e *password* , gli argomenti *userid* e *password* eseguiranno l'override dei valori specificati in *ConnectionString*.  
  
 Una volta terminate le operazioni su una **connessione**aperta, utilizzare il metodo [Close](../../../ado/reference/ado-api/close-method-ado.md) per liberare tutte le risorse di sistema associate. La chiusura di un oggetto non comporta la rimozione dalla memoria; è possibile modificare le impostazioni delle proprietà e usare il metodo **Open** per aprirlo di nuovo in un secondo momento. Per eliminare completamente un oggetto dalla memoria, impostare la variabile oggetto su *Nothing*.  
  
> [!NOTE]
>  **Utilizzo servizio dati remoto** Quando viene utilizzato su un oggetto **connessione** lato client, il metodo **Open** non stabilisce effettivamente una connessione al server fino a quando non viene aperto un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) nell'oggetto **Connection** .  
  
> [!NOTE]
>  Gli URL che usano lo schema http richiameranno automaticamente il [provider di Microsoft OLE DB per la pubblicazione Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per ulteriori informazioni, vedere [URL assoluto e relativo](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Esempio di metodi Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Esempio di metodi Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Metodo Open (record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Metodo Open (recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Metodo Open (flusso ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Metodo OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
