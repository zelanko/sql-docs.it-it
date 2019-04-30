---
title: Metodo Open (Record ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4d105d648c7877e7099dea637c2a2c6a094985f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241092"
---
# <a name="open-method-ado-record"></a>Metodo Open (Record - ADO)
Apre un oggetto esistente [Record](../../../ado/reference/ado-api/record-object-ado.md) dell'oggetto oppure crea un nuovo elemento rappresentato dalle **Record**, ad esempio un file o directory.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>Parametri  
 *Origine*  
 Facoltativo. Oggetto **Variant** che può rappresentare l'URL dell'entità per essere rappresentato da questa **Record** oggetto, una **comando**, un elemento aperto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o un'altra **Record** object, una stringa che contiene un'istruzione SQL SELECT o un nome di tabella.  
  
 *ActiveConnection*  
 Facoltativo. Oggetto **Variant** che rappresenta la stringa di connessione o open [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto.  
  
 *Mode*  
 Facoltativo. Oggetto [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valore che specifica la modalità di accesso per i risultanti **Record** oggetto. Valore predefinito è **adModeUnknown**.  
  
 *CreateOptions*  
 Facoltativo. Oggetto [RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md) valore che specifica se un file o directory deve essere aperta o se deve essere creata un nuovo file o directory. Valore predefinito è **adFailIfNotExists**. Se impostato sul valore predefinito, la modalità di accesso viene ottenuta dal [modalità](../../../ado/reference/ado-api/mode-property-ado.md) proprietà. Questo parametro viene ignorato quando le *origine* parametro non contiene un URL.  
  
 *Opzioni*  
 Facoltativo. Oggetto [RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md) valore che specifica le opzioni per l'apertura di **Record**. Valore predefinito è **adOpenRecordUnspecified dell'oggetto**. Questi valori possono essere combinati.  
  
 *UserName*  
 Facoltativo. Oggetto **stringa** valore contenente l'ID utente, se necessario, autorizza l'accesso al *origine*.  
  
 *Password*  
 Facoltativo. Oggetto **stringa** valore contenente la password, se necessario, verifica *UserName*.  
  
## <a name="remarks"></a>Note  
 *Origine* potrebbe essere:  
  
-   UN URL. Se il protocollo per l'URL è http, il Provider Internet verrà richiamato per impostazione predefinita. Se l'URL punta a un nodo che contiene uno script eseguibile (ad esempio un. Pagina ASP), un **Record** che contiene l'origine invece eseguito contenuto viene aperto per impostazione predefinita. Usare la *opzioni* argomento per modificare questo comportamento.  
  
-   Oggetto **Record** oggetto. Oggetto **Record** oggetto aperto da un'altra **Record** duplicherà originale **Record** oggetto.  
  
-   Oggetto **comando** oggetto. Aperta **Record** oggetto rappresenta la singola riga restituita eseguendo il **comando**. Se i risultati contengono più di una singola riga, il contenuto della prima riga viene inserito nel record e può essere aggiunto un errore per il **errori** raccolta.  
  
-   Un'istruzione SQL SELECT. Aperta **Record** oggetto rappresenta la singola riga restituita eseguendo il contenuto della stringa. Se i risultati contengono più di una singola riga, il contenuto della prima riga viene inserito nel record e può essere aggiunto un errore per il **errori** raccolta.  
  
-   Un nome di tabella.  
  
 Se il **Record** oggetto rappresenta un'entità che non è accessibile con un URL (ad esempio, una riga di un **Recordset** derivato da un database), i valori di entrambi i [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)proprietà e il campo cui si accede con il **adRecordURL** costante sono null.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Open (connessione ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Metodo Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Metodo OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
