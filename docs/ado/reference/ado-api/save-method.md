---
title: Metodo Save | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ec1601749b6537484cead17c50492de131932ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931178"
---
# <a name="save-method"></a>Metodo Save
Salva il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) in un file o [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>Parametri  
 *Destinazione*  
 facoltativo. Oggetto **Variant** che rappresenta il nome del percorso completo del file in cui le **Recordset** deve essere salvato, o un riferimento a una **Stream** oggetto.  
  
 *PersistFormat*  
 facoltativo. Oggetto [PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md) valore che specifica il formato in cui le **Recordset** devono essere salvati (XML o ADTG). Il valore predefinito è **adPersistADTG**.  
  
## <a name="remarks"></a>Note  
 Il [metodo Save](../../../ado/reference/ado-api/save-method.md) metodo può essere richiamato solo su un elemento aperto **Recordset**. Usare la [metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo di ripristino successive il **Recordset** dalla *destinazione*.  
  
 Se il [proprietà Filter](../../../ado/reference/ado-api/filter-property.md) proprietà è valida per il **Recordset**, quindi vengono salvate solo le righe accessibili in base al filtro. Se il **Recordset** è di tipo gerarchico, quindi il membro figlio corrente **Recordset** e i relativi elementi figlio viene salvati, incluso l'elemento padre **Recordset**. Se il metodo Save di un elemento figlio **Recordset** viene chiamato, l'elemento figlio e i relativi elementi figlio viene salvati, ma non è l'elemento padre.  
  
 La prima volta che salva il **Recordset**, è possibile specificare facoltativamente *destinazione*. Se si omette *destinazione*, verrà creato un nuovo file con un nome impostato sul valore della proprietà dell'origine delle **Recordset**.  
  
 Omettere *destinazione* quando si chiama successivamente **salvare** dopo il primo salvataggio o un errore di run-time si verificherà. Se successivamente si chiama **salvare** con un nuovo oggetto *destinazione*, il **Recordset** viene salvato nella nuova destinazione. Tuttavia, la nuova destinazione e la destinazione originale entrambi saranno aperte.  
  
 **Salvare** non chiude il **Recordset** o *destinazione*, quindi è possibile continuare a lavorare con i **Recordset** e salvare le modifiche più recenti. *Destinazione* rimane aperta fino a quando il **Recordset** viene chiuso.  
  
 Per motivi di sicurezza, il **salvare** metodo consente solo l'uso delle impostazioni di sicurezza personalizzato e basso da uno script eseguito da Microsoft Internet Explorer.  
  
 Se il **salvare** viene chiamato durante un'asincrona **Recordset** recuperare, eseguire o aggiornare operazione è in corso, quindi **Salva** attende che l'operazione asincrona è stata completata.  
  
 Vengono salvati i record che iniziano con la prima riga del **Recordset**. Quando la **salvare** metodo termina, la posizione della riga corrente viene spostata sulla prima riga del **Recordset**.  
  
 Per ottenere risultati ottimali, impostare il [proprietà CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà **adUseClient** con **Salva**. Se il provider non supporta tutte le funzionalità necessarie per salvare **Recordset** oggetti, il servizio di cursore fornirà tale funzionalità.  
  
 Quando un **Recordset** persistente con il **CursorLocation** proprietà impostata su **adUseServer**, la funzionalità di aggiornamento per il **Recordset**è limitato. In genere, solo tabella singola aggiornamenti, inserimenti ed eliminazioni sono consentite (dipenderà dalle funzionalità del provider). Il [metodo Resync](../../../ado/reference/ado-api/resync-method.md) metodo è anche disponibile in questa configurazione.  
  
> [!NOTE]
>  Salvataggio di un **Recordset** con **campi** di tipo **adVariant**, **adIDispatch**, o **adIUnknown** è non è supportato da ADO e può causare risultati imprevedibili.  
  
 Consente di filtrare solo sotto forma di stringhe di criteri (ad esempio DataOrdine > ' 12/31/1999 ') influiscono sul contenuto di un persistente **Recordset**. I filtri creati con una matrice di **segnalibri** o usando un valore compreso il [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) non influirà il contenuto della classe resa persistente **Recordset**. Queste regole si applicano ai **Recordset**creati con i cursori lato client o lato server.  
  
 Poiché il *destinazione* parametro può accettare qualsiasi oggetto che supporta l'interfaccia IStream OLE DB, è possibile salvare una **Recordset** direttamente per l'oggetto risposta ASP. Per altre informazioni, vedere la **Scenario di persistenza Recordset XML**.  
  
 È inoltre possibile salvare una **Recordset** in formato XML a un'istanza di un oggetto DOM MSXML, come è illustrato nel codice Visual Basic seguente:  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=Northwind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistXML   'Save Recordset directly into a DOM tree.  
...  
```  
  
> [!NOTE]
>  Due limitazioni si applicano quando si salva il recordset gerarchici (forme di dati) in formato XML. Se non è possibile salvare in XML la gerarchica **Recordset** include aggiornamenti, in sospeso e non è possibile salvare un con parametri gerarchici **Recordset**.  
  
 Oggetto **Recordset** salvati in formato XML formato viene salvato usando il formato UTF-8. Quando tale file viene caricato in un Stream ADO, l'oggetto Stream non tenterà di aprire una **Recordset** dal flusso, a meno che la proprietà set di caratteri del flusso è impostata sul valore appropriato per il formato UTF-8.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Salvare e aprire l'esempio di metodi (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Salvare e aprire l'esempio di metodi (VC + +)](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Metodo Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Metodo SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
