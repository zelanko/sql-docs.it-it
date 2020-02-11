---
title: Servizio Data Shaping Microsoft per OLE DB (provider di servizi ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ddef2feab633627c9549b73787faa1d104d69c5e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926814"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Panoramica di Microsoft Data Shaping Service per OLE DB
> [!IMPORTANT]
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Al contrario, le applicazioni devono utilizzare XML.

 Il servizio di data shaping Microsoft per OLE DB provider di servizi supporta la costruzione di oggetti [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) gerarchici (a forma di) da un provider di dati.

## <a name="provider-keyword"></a>Parola chiave provider
 Per richiamare il servizio Data Shaping per OLE DB, specificare la parola chiave e il valore seguenti nella stringa di connessione.

```vb
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>Proprietà dinamiche
 Quando il provider di servizi viene richiamato, le seguenti proprietà dinamiche vengono aggiunte alla raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) dell'oggetto[Connection](../../../ado/reference/ado-api/connection-object-ado.md) .

|Nome proprietà dinamica|Descrizione|
|---------------------------|-----------------|
|**Nomi di riforme univoci**|Indica se sono consentiti oggetti **Recordset** con valori duplicati per le proprietà del nome di modifica della **forma** . Se questa proprietà dinamica è **true** e viene creato un nuovo **Recordset** con lo stesso nome di modifica della forma specificato dall'utente come **Recordset**esistente, il nome della nuova forma dell'oggetto **Recordset** viene modificato per renderlo univoco. Se questa proprietà è **false** e viene creato un nuovo **Recordset** con lo stesso nome di modifica della forma specificato dall'utente del **Recordset**esistente, entrambi gli oggetti **Recordset** avranno lo stesso nome di modifica della forma. Non è pertanto possibile modificare la forma di un **Recordset** purché siano presenti entrambi i recordset.<br /><br /> Il valore predefinito della proprietà è **false**.|
|**Provider di dati**|Indica il nome del provider che fornirà le righe da modellare. Questo valore può essere NONE se non viene utilizzato un provider per fornire righe.|

 È inoltre possibile impostare le proprietà dinamiche scrivibili specificandone i nomi come parole chiave nella stringa di connessione. Ad esempio, in Microsoft Visual Basic impostare la proprietà dinamica **provider di dati** su "MSDASQL" specificando:

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 È anche possibile impostare o recuperare una proprietà dinamica specificandone il nome come indice della proprietà [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) . Ad esempio, l'esempio di codice seguente ottiene e stampa il valore corrente della proprietà dinamica **provider di dati** , quindi imposta un nuovo valore se cn. Datafornitor è stato impostato su "MSDataShape" (in modo diretto o indiretto tramite la stringa di connessione) e la connessione non è stata aperta:

```vb
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  La proprietà dinamica, **provider di dati**, può essere impostata solo su un oggetto **connessione** non aperto. Una volta aperta la connessione, la proprietà **provider di dati** diventa di sola lettura.

 Per ulteriori informazioni sulla data shaping, vedere [data shaping](../../../ado/guide/data/data-shaping-overview.md).

## <a name="see-also"></a>Vedere anche
 [Appendice A: Provider](../../../ado/guide/appendixes/appendix-a-providers.md)
