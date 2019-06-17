---
title: Proprietà ActiveConnection (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0f423eb2d06ccdc925402d0db5d8a459f7ffdd5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698922"
---
# <a name="activeconnection-property-ado"></a>Proprietà ActiveConnection (ADO)
Indica a quale [Connection](../../../ado/reference/ado-api/connection-object-ado.md) dell'oggetto specificato [comando](../../../ado/reference/ado-api/command-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), oppure [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto appartiene attualmente.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** che contiene una definizione per una connessione se la connessione viene chiusa, o un valore **Variant** contenente corrente **connessione** oggetto se la la connessione è aperta. Valore predefinito è un riferimento a un oggetto null. Vedere le [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà.  
  
## <a name="remarks"></a>Note  
 Usare la **ActiveConnection** proprietà per determinare le **connessione** oggetto su cui specificato **comando** verrà eseguito l'oggetto o l'oggetto specificato  **Recordset** verrà aperto.  
  
## <a name="command"></a>Comando  
 Per la **comandi** oggetti, il **ActiveConnection** è di lettura/scrittura.  
  
 Se si prova a chiamare le [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) metodo su un **comando** oggetto prima di impostare questa proprietà su un elemento aperto **connessione** oggetto o stringa di connessione valida, si verifica un errore.  
  
 Se un **Connection** oggetto viene assegnato alle **ActiveConnection** proprietà, l'oggetto deve essere aperto. Assegnazione di un oggetto connessione chiuso provoca un errore.  
  
### <a name="note"></a>Nota  
 **Microsoft Visual Basic** impostazione il **ActiveConnection** proprietà *Nothing* Dissocia il **comando** oggetto dall'insieme corrente **Connessione** e fa sì che il provider di rilasciare le risorse associate per l'origine dati. È quindi possibile associare il **comandi** oggetto con lo stesso o in un'altra **connessione** oggetto. Alcuni provider consentono di modificare l'impostazione della proprietà da una **Connection** a un altro, senza dover prima di tutto impostare la proprietà su *Nothing*.  
  
 Se il [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) insieme delle **comando** oggetto contiene i parametri forniti dal provider, la raccolta viene cancellata se si imposta la **ActiveConnection** proprietà da *Nothing* o a un'altra **connessione** oggetto. Se si creano manualmente [parametro](../../../ado/reference/ado-api/parameter-object.md) degli oggetti e usarli per riempire il **parametri** raccolta del **comando** oggetto, impostando il **ActiveConnection**  proprietà *Nothing* o a un altro **connessione** oggetto lascia il **parametri** raccolta intatto.  
  
 Chiusura di **connessione** oggetto con cui un **comando** oggetto è set associati il **ActiveConnection** proprietà *Nothing*. Impostando questa proprietà su un oggetto chiuso **connessione** oggetto genera un errore.  
  
## <a name="recordset"></a>recordset  
 Per aprire **Recordset** oggetti o per **Recordset** oggetti la cui proprietà [origine](../../../ado/reference/ado-api/source-property-ado-recordset.md) proprietà è impostata su un valore valido **comando** oggetto, il **ActiveConnection** proprietà è di sola lettura. In caso contrario, è di lettura/scrittura.  
  
 È possibile impostare questa proprietà su un valore valido **connessione** oggetto o a una stringa di connessione valida. In questo caso, il provider crea un nuovo **connessione** utilizzando questa definizione dell'oggetto e viene aperta la connessione. Inoltre, il provider può impostare questa proprietà per il nuovo **connessione** oggetto per offrirti un modo per accedere la **connessione** per informazioni dettagliate sull'errore o di eseguire altri comandi dell'oggetto.  
  
 Se si usa il *ActiveConnection* argomento del [aprire](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo per aprire un **Recordset** oggetto, il **ActiveConnection** sarà di proprietà ereditare il valore dell'argomento.  
  
 Se si imposta la **origine** proprietà delle **Recordset** oggetto su un valore valido **comando** variabile oggetto, il **ActiveConnection** proprietà di il **Recordset** eredita l'impostazione delle **comando** dell'oggetto **ActiveConnection** proprietà.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** quando viene usato in un client-side **Recordset** dell'oggetto, questa proprietà può essere impostata solo su una stringa di connessione o (in Microsoft Visual Basic o Visual Basic, Scripting Edition) a *Nothing* .  
  
## <a name="record"></a>Record  
 Questa proprietà è di lettura/scrittura quando il **Record** oggetto è chiuso e può contenere una stringa di connessione o un riferimento a un elemento aperto **connessione** oggetto. Questa proprietà è di sola lettura quando le **Record** oggetto è aperto e contiene un riferimento a un elemento aperto **connessione** oggetto.  
  
 Oggetto **Connection** oggetto viene creato in modo implicito quando le **Record** apertura dell'oggetto da un URL. Aprire il **Record** con un oggetto esistente, aprire **connessione** oggetto assegnando il **connessione** dell'oggetto a questa proprietà o tramite il **connessione** oggetto come parametro nel [Open](../../../ado/reference/ado-api/open-method-ado-record.md) chiamata al metodo. Se il **Record** viene aperto da un oggetto esistente **Record** o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), quindi è automaticamente associato a tale **Record** o  **Recordset** dell'oggetto **connessione** oggetto.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione (esempio di proprietà (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni ed esempio di proprietà direzione (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione (esempio di proprietà (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Proprietà ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)
