---
title: Oggetto Cell (ADO MD) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d309ba98c1e50d8eb6fbe47fb9452f8ea7df35ba
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761799"
---
# <a name="cell-object-ado-md"></a>Oggetto Cell (ADO MD)
Rappresenta i dati all'intersezione delle coordinate dell'asse contenute in un oggetto Cell.  
  
## <a name="remarks"></a>Osservazioni  
 Un oggetto **cella** viene restituito dalla proprietà [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) di un oggetto [cellt](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) .  
  
 Con le raccolte e le proprietà di un oggetto **cella** , è possibile eseguire le operazioni seguenti:  
  
-   Restituire i dati nella **cella** con la proprietà [value](../../../ado/reference/ado-md-api/value-property-ado-md.md) .  
  
-   Restituisce la stringa che rappresenta la visualizzazione formattata della proprietà **value** con la proprietà [formattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md) .  
  
-   Restituisce il valore ordinale della **cella** all'interno del **cella con la** proprietà [ordinale](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md) .  
  
-   Determinare la posizione della **cella** all'interno di [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) con la raccolta [Positions](../../../ado/reference/ado-md-api/positions-collection-ado-md.md) .  
  
-   Recuperare altre informazioni sulla **cella** con la raccolta delle [Proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) ADO standard.  
  
 La raccolta **Properties** contiene proprietà fornite dal provider. Nella tabella seguente sono elencate le proprietà che potrebbero essere disponibili. L'elenco di proprietà effettivo può variare a seconda dell'implementazione del provider. Per un elenco più completo delle proprietà disponibili, vedere la documentazione relativa al provider.  
  
|Nome|Description|  
|----------|-----------------|  
|ColoreSfondo|Colore di sfondo utilizzato per la visualizzazione della cella.|  
|FontFlags|Maschera di maschera che illustra in dettaglio gli effetti sul tipo di carattere.|  
|FontName|Tipo di carattere utilizzato per visualizzare il valore della cella.|  
|FontSize|Dimensioni del carattere utilizzate per visualizzare il valore della cella.|  
|ColorePrimoPiano|Colore di primo piano utilizzato per la visualizzazione della cella.|  
|FormatString|Valore in una stringa formattata.|  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di asse (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Oggetto cellt (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Raccolta Positions (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
