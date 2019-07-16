---
title: CursorTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6333934997c9de38b8df1dd08849886ff3dd7f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933278"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
Specifica il tipo di cursore utilizzato una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|Usa un cursore dinamico. Aggiunte, modifiche ed eliminazioni da altri utenti sono visibili e tutti i tipi di spostamento all'interno di **Recordset** sono consentiti, ad eccezione dei segnalibri, se il provider non li supporta.|  
|**adOpenForwardOnly**|0|Valore predefinito. Usa un cursore forward-only. Identico a un cursore statico, ad eccezione del fatto che può solo lo scorrimento in avanti di record. Ciò migliora le prestazioni quando è necessario apportare solo una passano attraverso un **Recordset**.|  
|**adOpenKeyset**|1|Usa un cursore keyset. Ad esempio un cursore dinamico, ad eccezione del fatto che non è possibile visualizzare i record aggiunti da altri utenti, anche se i record eliminati dagli altri utenti non sono accessibili dalle **Recordset**. Le modifiche ai dati da altri utenti sono ancora visibili.|  
|**adOpenStatic**|3|Usa un cursore statico, ovvero una copia statica di un set di record che è possibile usare per trovare i dati o per generare i report. Le aggiunte, modifiche o eliminazioni da altri utenti non sono visibili.|  
|**adOpenUnspecified**|-1|Non specifica il tipo di cursore.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.CursorType.DYNAMIC|  
|AdoEnums.CursorType.FORWARDONLY|  
|AdoEnums.CursorType.KEYSET|  
|AdoEnums.CursorType.STATIC|  
|AdoEnums.CursorType.UNSPECIFIED|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
