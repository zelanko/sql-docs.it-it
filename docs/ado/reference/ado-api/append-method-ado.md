---
title: Metodo Append (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 987b7d7006ff448a92eee1926a2c60c3b7ae039e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696673"
---
# <a name="append-method-ado"></a>Metodo Append (ADO)
Aggiunge un oggetto a una raccolta. Se la raccolta è [i campi](../../../ado/reference/ado-api/fields-collection-ado.md), un nuovo [campo](../../../ado/reference/ado-api/field-object.md) oggetto può essere creato prima di essere aggiunta alla raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>Parametri  
 *collection*  
 Oggetto raccolta.  
  
 *fields*  
 Oggetto **campi** raccolta.  
  
 *object*  
 Una variabile oggetto che rappresenta l'oggetto da aggiungere.  
  
 *Name*  
 Oggetto **stringa** valore contenente il nome del nuovo **campo** dell'oggetto e non deve essere lo stesso nome come qualsiasi altro oggetto nel *campi*.  
  
 *Tipo*  
 Oggetto [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valore, il cui valore predefinito è **adEmpty**, che specifica il tipo di dati del nuovo campo. Tipi di dati seguenti non sono supportati da ADO e dovrebbe non essere utilizzato quando Accodamento di nuovi campi a un [Recordset ADO (Object)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**, **adIUnknown**, **adVariant**.  
  
 *DefinedSize*  
 Facoltativo. Oggetto **lungo** valore che rappresenta la dimensione definita, in caratteri o byte, del nuovo campo. Il valore predefinito per questo parametro viene derivato dalla *tipo*. Campi che dispongono di un *DefinedSize* maggiori di 255 byte vengono gestite come colonne a lunghezza variabile. Il valore predefinito per *DefinedSize* non è specificato.  
  
 *Attrib*  
 Facoltativo. Oggetto [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) valore, il cui valore predefinito è **adFldDefault**, che specifica gli attributi per il nuovo campo. Se questo valore viene omesso, il campo conterrà gli attributi derivati da *tipo*.  
  
 *FieldValue*  
 Facoltativo. Oggetto **Variant** che rappresenta il valore per il nuovo campo. Se non specificato, il campo viene aggiunto con un valore null.  
  
## <a name="remarks"></a>Note  
  
## <a name="parameters-collection"></a>Raccolta Parameters  
 È necessario impostare il [tipo](../../../ado/reference/ado-api/type-property-ado.md) proprietà di un [parametro](../../../ado/reference/ado-api/parameter-object.md) oggetto prima di aggiungerlo al [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) raccolta. Se si seleziona un tipo di dati a lunghezza variabile, è necessario impostare anche il [dimensioni](../../../ado/reference/ado-api/size-property-ado-parameter.md) proprietà su un valore maggiore di zero.  
  
 Che descrive i parametri manualmente riduce al minimo le chiamate al provider e pertanto migliora le prestazioni quando si utilizzano le stored procedure o query con parametri. Tuttavia, è necessario conoscere le proprietà dei parametri associati con la stored procedure o con parametri di query che si vuole chiamare.  
  
 Usare la [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) metodo per creare **parametro** oggetti con le impostazioni di proprietà appropriata e usare il **Append** metodo a cui aggiungere i il [ Parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) raccolta. Ciò consente di impostare e restituire i valori dei parametri senza la necessità di chiamare il provider per le informazioni sui parametri. Se si scrive in un provider che non fornisce informazioni sui parametri, è necessario utilizzare questo metodo per compilare manualmente la **parametri** insieme per poter utilizzare i parametri.  
  
## <a name="fields-collection"></a>Raccolta Fields  
 Il *FieldValue* parametro è valido solo quando si aggiunge un **campo** dell'oggetto a una [Record](../../../ado/reference/ado-api/record-object-ado.md) dell'oggetto, non a un **Recordset** oggetto. Con un **Record** dell'oggetto, è possibile aggiungere campi e specificare i valori nello stesso momento. Con un **Recordset** dell'oggetto, è necessario creare campi durante le **Recordset** è chiuso e quindi aprire il **Recordset** e assegnare valori ai campi.  
  
> [!NOTE]
>  Per ottenere nuove **campo** gli oggetti che sono stati accodati per il **campi** raccolta di un **Record** oggetto, il [valore](../../../ado/reference/ado-api/value-property-ado.md) deve essere impostata prima di qualsiasi altro **campo** proprietà possono essere specificate. Per prima cosa, un valore specifico per il **valore** proprietà necessario aver assegnata e [Update](../../../ado/reference/ado-api/update-method.md) sul **campi** raccolta denominata. Quindi, le altre proprietà, ad esempio [tipo](../../../ado/reference/ado-api/type-property-ado.md) oppure [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) sono accessibili. **Campo** oggetti dei seguenti tipi di dati (**DataTypeEnum**) non possono essere accodati per il **campi** raccolta e causerà un errore si verifica: **adArray**, **adChapter**, **adEmpty**, **adPropVariant**, e **adUserDefined**. Inoltre, i tipi di dati seguenti non sono supportati da ADO: **adIDispatch**, **adIUnknown**, e **adIVariant**. Per questi tipi, nessun errore si verifica quando aggiunto, ma utilizzo può produrre risultati imprevisti, tra cui le perdite di memoria.  
  
## <a name="recordset"></a>recordset  
 Se non si imposta la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà prima di chiamare il **Append** metodo **CursorLocation** verrà impostato su **adUseClient** ( una [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) valore) automaticamente quando il [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo per il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) viene chiamato l'oggetto.  
  
 Se si verificherà un errore di run-time di **Append** metodo viene chiamato sul **campi** raccolta di un elemento aperto **Recordset**, o in un **Recordset** in cui il [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) proprietà è stata impostata. È possibile aggiungere solo i campi da un **Recordset** che non è aperta e non è ancora stato connesso a un'origine dati. Ciò avviene in genere quando un **Recordset** oggetto viene creato con il [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) metodo o assegnato a una variabile oggetto.  
  
## <a name="record"></a>Record  
 Errore di run-time non si verificherà se il **Append** metodo viene chiamato sulle **campi** raccolta di un elemento aperto **Record**. Verrà aggiunto il nuovo campo per il **i campi** insieme delle **Record** oggetto. Se il **Record** fu derivata da una **Recordset**, il nuovo campo non compariranno nella **campi** raccolta del **Recordset** oggetto.  
  
 Può essere creato e aggiunto a un campo inesistente il **campi** raccolta assegnando un valore per l'oggetto campo, come se esistesse già nella raccolta. L'assegnazione verrà attivata la creazione automatica e l'aggiunta del **campo** oggetto e quindi l'assegnazione verrà completata.  
  
 Dopo aver aggiunto un **campo** per il **campi** raccolta di un **Record** dell'oggetto, chiamare il **Update** metodo del **campi**  insieme per salvare le modifiche.  
  
## <a name="applies-to"></a>Si applica a  
  
- [Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Raccolta di parametri (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Append e CreateParameter (esempio di metodi (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append e CreateParameter metodi (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Metodo CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Metodo Delete (raccolta Fields ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Metodo Delete (insieme di parametri ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Elimina metodo (Recordset ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Metodo Update](../../../ado/reference/ado-api/update-method.md)
