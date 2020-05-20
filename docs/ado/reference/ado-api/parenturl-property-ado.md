---
title: Proprietà ParentURL (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
author: rothja
ms.author: jroth
ms.openlocfilehash: cb0669abc03da183fc70c289631fed67bb41829d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761989"
---
# <a name="parenturl-property-ado"></a>Proprietà ParentURL (ADO)
Indica una stringa URL assoluta che punta al [record](../../../ado/reference/ado-api/record-object-ado.md) padre dell'oggetto **record** corrente.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **stringa** che indica l'URL del **record**padre.  
  
## <a name="remarks"></a>Osservazioni  
 La proprietà **ParentURL** dipende dall'origine utilizzata per aprire l'oggetto **record** . Ad esempio, è possibile aprire il **record** con un'origine contenente un percorso relativo di una directory a cui fa riferimento la proprietà [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) .  
  
 Si supponga che "Second" sia una cartella contenuta in "First". Aprire l'oggetto **record** utilizzando la sintassi seguente:  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 A questo punto, il valore della `the` proprietà **ParentURL** è `"https://first"` uguale a **ActiveConnection**.  
  
 L'origine può anche essere un URL assoluto, ad esempio, `"https://first/second"` . La proprietà **ParentURL** è quindi `"https://first"` il livello precedente `"second"` .  
  
 Questa proprietà può essere un valore null se:  
  
-   Nessun elemento padre per l'oggetto corrente. ad esempio, se l'oggetto **record** rappresenta la radice di una directory.  
  
-   L'oggetto **record** rappresenta un'entità che non può essere specificata con un URL.  
  
 Questa proprietà è di sola lettura.  
  
> [!NOTE]
>  Questa proprietà è supportata solo dai provider di origine del documento, ad esempio il [provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per ulteriori informazioni, vedere [record e campi forniti dal provider](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
> [!NOTE]
>  Gli URL che usano lo schema http richiameranno automaticamente il [provider di Microsoft OLE DB per la pubblicazione Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per ulteriori informazioni, vedere [URL assoluto e relativo](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
> [!NOTE]
>  Se il record corrente contiene un record di dati di un **Recordset**ADO, l'accesso alla proprietà **ParentURL** genera un errore di run-time, a indicare che non è possibile alcun URL.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
