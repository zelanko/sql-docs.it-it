---
title: Oggetto (ADO MD) Cell | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell
helpviewer_keywords:
- Cell object [ADO MD]
ms.assetid: dcc2f044-b785-4a29-9bc5-b673f66eedf9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df7b93e00ddff15c320152e3fa2bc1f104caa3a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469486"
---
# <a name="cell-object-ado-md"></a>Oggetto Cell (ADO MD)
Rappresenta i dati in corrispondenza dell'intersezione delle coordinate dell'asse contenuti in un set di celle.  
  
## <a name="remarks"></a>Note  
 Oggetto **cella** viene restituito dalle [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) proprietà di un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) oggetto.  
  
 Con le raccolte e le proprietà di un **cella** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Restituire i dati nel **cella** con il [valore](../../../ado/reference/ado-md-api/value-property-ado-md.md) proprietà.  
  
-   Restituire la stringa che rappresenta la visualizzazione formattata delle **valore** proprietà con il [FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md) proprietà.  
  
-   Restituire il valore ordinale del **cella** all'interno di **set di celle** con il [ordinale](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md) proprietà.  
  
-   Determinano la posizione del **cella** all'interno di [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) con il [posizioni](../../../ado/reference/ado-md-api/positions-collection-ado-md.md) raccolta.  
  
-   Recuperare altre informazioni sui **cella** con l'oggetto ADO standard [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
 Il **proprietà** raccolta contiene le proprietà specifiche del provider. La tabella seguente elenca le proprietà che potrebbero essere disponibili. L'elenco di proprietà effettivo può variare in base all'implementazione del provider. Vedere la documentazione per il provider per un elenco completo delle proprietà disponibili.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|ColoreSfondo|Colore di sfondo utilizzato durante la visualizzazione della cella.|  
|FontFlags|Maschera di bit che riporta in dettaglio gli effetti sul tipo di carattere.|  
|TipoCarattere|Tipo di carattere utilizzato per visualizzare il valore della cella.|  
|FontSize|Dimensioni del carattere utilizzata per visualizzare il valore della cella.|  
|ColorePrimoPiano|Colore di primo piano usato durante la visualizzazione della cella.|  
|FormatString|Valore in una stringa formattata.|  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Axis (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Raccolta Positions (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
