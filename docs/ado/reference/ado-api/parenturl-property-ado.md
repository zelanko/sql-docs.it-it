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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 65704cea2a396e0f03de4bbcdc9f031f4c9af583
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703462"
---
# <a name="parenturl-property-ado"></a>Proprietà ParentURL (ADO)
Indica una stringa URL assoluto che punta all'elemento padre [Record](../../../ado/reference/ado-api/record-object-ado.md) dell'oggetto corrente **Record** oggetto.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **stringa** valore che indica l'URL dell'elemento padre **Record**.  
  
## <a name="remarks"></a>Note  
 Il **ParentURL** proprietà dipende dall'origine consente di aprire le **Record** oggetto. Ad esempio, il **Record** possono essere aperti con un'origine che contiene un nome di percorso relativo di una directory a cui fanno riferimento le [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) proprietà.  
  
 Si supponga che "second" è una cartella inclusa in "first". Aprire il **Record** oggetto usando la sintassi seguente:  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 A questo punto, il valore di `the` **ParentURL** è di proprietà `"https://first"`, la stessa come **ActiveConnection**.  
  
 L'origine può anche essere un URL assoluto, ad esempio, `"https://first/second"`. Il **ParentURL** proprietà viene quindi `"https://first"`, il livello superiore `"second"`.  
  
 Questa proprietà può essere un valore null se:  
  
-   Non vi è alcun elemento padre dell'oggetto corrente; ad esempio, se il **Record** oggetto rappresenta la radice di una directory.  
  
-   Il **Record** oggetto rappresenta un'entità che non può essere specificata con un URL.  
  
 Questa proprietà è di sola lettura.  
  
> [!NOTE]
>  Questa proprietà è supportata solo dai provider di origine di documento, ad esempio la [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [record e campi specificati dal provider](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
> [!NOTE]
>  Se il record corrente contiene un record di dati da un oggetto ADO **Recordset**, l'accesso alla **ParentURL** proprietà causa un errore di run-time, che indica che non è possibile utilizzare alcun URL.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
