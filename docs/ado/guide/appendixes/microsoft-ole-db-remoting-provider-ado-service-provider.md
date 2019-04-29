---
title: Provider di servizi remoti Microsoft OLE DB (ADO Service Provider) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29addb89a5713b32b98df374a673fff4d549d771
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62853453"
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Panoramica di Provider Microsoft OLE DB remota
Il Provider .NET Remoting Microsoft OLE DB consente a un utente locale in un computer client richiamare i provider di dati in un computer remoto. Come si farebbe se trattasse di un utente locale nel computer remoto, specificare i parametri del provider di dati per il computer remoto. Quindi specificare i parametri utilizzati dal Provider di servizi remoti di accedere al computer remoto. È quindi possibile accedere nel computer remoto come se trattasse di un utente locale.

> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).

## <a name="provider-keyword"></a>Parola chiave provider
 Per richiamare il Provider OLE DB remota, specificare la parola chiave e il valore seguenti nella stringa di connessione. Si noti lo spazio vuoto nel nome del provider.

```vb
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>Parole chiave aggiuntive
 Quando viene richiamato questo provider di servizi, le parole chiave aggiuntive seguenti sono rilevanti.

|Parola chiave|Descrizione|
|-------------|-----------------|
|**Data Source**|Specifica il nome dell'origine dati remota. Viene passato al provider OLE DB .NET Remoting per l'elaborazione.<br /><br /> Questa parola chiave è equivalente al [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) dell'oggetto [Connect](../../../ado/reference/rds-api/connect-property-rds.md) proprietà.|

## <a name="dynamic-properties"></a>Proprietà dinamiche
 Quando viene richiamato questo provider di servizi, le seguenti proprietà dinamiche vengono aggiunti per il [Connection](../../../ado/reference/ado-api/connection-object-ado.md)dell'oggetto [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.

|Nome della proprietà dinamica|Descrizione|
|---------------------------|-----------------|
|**DFMode**|Indica la modalità di data factory. Stringa che specifica la versione desiderata del [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) oggetto nel server. Impostare questa proprietà prima di aprire una connessione per richiedere una versione specifica del **DataFactory**. Se la versione richiesta non è disponibile, è verrà effettuato un tentativo di utilizzare la versione precedente. Se è presente alcuna versione precedente, si verificherà un errore. Se **DFMode** è inferiore alla versione disponibile, si verificherà un errore. Questa proprietà è di sola lettura dopo aver stabilita una connessione.<br /><br /> Può essere uno dei seguenti valori di stringa valida:<br /><br /> -"25"-versione 2.5 (impostazione predefinita)<br />-"21"-la versione 2.1<br />-"20"-versione 2.0<br />-"15"-la versione 1.5|
|**Proprietà dei comandi**|Indica i valori che verranno aggiunti alla stringa di proprietà dei comandi (set di righe) inviato al server dal provider di MS Remote. Il valore predefinito di questa stringa è vt_empty.|
|**DFMode corrente**|Indica il numero di versione effettiva dei **DataFactory** nel server. Questa proprietà per verificare se la versione richiesta nel **DFMode** proprietà è stata rispettata.<br /><br /> Può essere uno dei seguenti valori Long integer valido:<br /><br /> -25-version 2.5 (impostazione predefinita)<br />-21-versione 2.1<br />-20-versione 2.0<br />-15-version 1.5<br /><br /> Aggiunta di "DFMode = 20;" alla stringa di connessione quando si usa la **MSRemote** provider può migliorare le prestazioni del server durante l'aggiornamento dati. Con questa impostazione, il **RDSServer** oggetti sul server utilizza una modalità meno risorse. Tuttavia, le funzionalità seguenti non sono disponibili in questa configurazione:<br /><br /> -Uso di query con parametri.<br />-Recupero di informazioni di parametro o della colonna prima di chiamare il **Execute** (metodo).<br />-Impostazione **Transact Updates** al **True**.<br />-Recupero dello stato di riga.<br />-Chiamata di **Risincronizza** (metodo).<br />-Aggiornamento (in modo esplicito o automaticamente) tramite il **Update Resync** proprietà.<br />-Impostazione **comandi** oppure **Recordset** proprietà.<br />-Uso **adCmdTableDirect**.|
|**Handler**|Indica il nome del programma di personalizzazione lato server (o gestore) che estende le funzionalità dei [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)ed eventuali parametri utilizzati dal gestore *,* tutti separati da virgole ( ","). Valore **String**.|
|**Timeout Internet**|Indica il numero massimo di millisecondi di attesa per una richiesta venga trasmessa da e verso il server. (Il valore predefinito è 5 minuti).|
|**Provider remoto**|Indica il nome del provider di dati da utilizzare nel server remoto.|
|**Server remoto**|Indica il protocollo server, nome e la comunicazione da usare per questa connessione. Questa proprietà è equivalente al [Servizi Desktop remoto. DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetti [Server](../../../ado/reference/rds-api/server-property-rds.md) proprietà.|
|**Transact aggiornamenti**|Se impostato su **True**, questo valore indica che quando [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) viene eseguita nel server, verrà eseguita all'interno di una transazione. È il valore predefinito per questa proprietà dinamica booleana **False**.|

 È anche possibile impostare le proprietà dinamiche scrivibile specificando i relativi nomi come parole chiave nella stringa di connessione. Ad esempio, impostare il **Timeout Internet** proprietà dinamica su cinque secondi, specificando:

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 È anche possibile impostare o recuperare una proprietà dinamica specificandone il nome dell'indice per la **proprietà** proprietà. Nell'esempio seguente viene illustrato come ottenere e visualizzare il valore corrente del **Timeout Internet** proprietà dinamica e quindi impostare un nuovo valore:

```vb
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>Note
 In ADO 2.0, il Provider OLE DB remota potrebbe essere specificato solo nel *ActiveConnection* parametro delle [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto **Open** (metodo). A partire da ADO 2.1, il provider può anche essere specificato nel *ConnectionString* parametro delle [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto **Open** (metodo).

 L'equivalente del **Servizi Desktop remoto. DataControl** oggetti [SQL](../../../ado/reference/rds-api/sql-property.md) proprietà non è disponibile. Il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto **Open** metodo *origine* viene invece usato l'argomento.

 **Nota** specificando ".... Provider remoto = Remote MS;... "verrà creato uno scenario di quattro livelli. Scenario oltre a tre livelli non è stati testati e non sono necessari.

## <a name="example"></a>Esempio
 In questo esempio viene eseguita una query sulla **autori** tabella del **Pubs** database in un server denominato *server*. I nomi di origine dati remota e di server remoti sono incluse nel [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) metodo del[connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto e la query SQL viene specificata nel[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto. Oggetto **Recordset** oggetto viene restituito, modificato e utilizzato per aggiornare l'origine dati.

```vb
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=https://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>Vedere anche
 [Panoramica del Provider OLE DB per .NET Remoting](https://msdn.microsoft.com/4083b72f-68c4-4252-b366-abb70db5ca2b)
