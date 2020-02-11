---
title: Proprietà Size (parametro ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3796f772dedb961ec34eb0639034350989f99142
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931059"
---
# <a name="size-property-ado-parameter"></a>Proprietà Size (Parameter - ADO)
Indica la dimensione massima, in byte o caratteri, di un oggetto [Parameter](../../../ado/reference/ado-api/parameter-object.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** che indica la dimensione massima in byte o caratteri di un valore in un oggetto **Parameter** .  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **size** per determinare le dimensioni massime per i valori scritti o letti dalla proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) di un oggetto **Parameter** .  
  
 Se si specifica un tipo di dati a lunghezza variabile per un oggetto **Parameter** (ad esempio, qualsiasi tipo **stringa** , ad esempio **adVarChar**), è necessario impostare la proprietà **size** dell'oggetto prima di aggiungerlo alla raccolta [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) . in caso contrario, si verifica un errore.  
  
 Se è già stato aggiunto l'oggetto **Parameter** alla raccolta **Parameters** di un oggetto [Command](../../../ado/reference/ado-api/command-object-ado.md) e il tipo viene modificato in un tipo di dati a lunghezza variabile, è necessario impostare la proprietà **size** dell'oggetto **Parameter** prima di eseguire l'oggetto **Command** . in caso contrario, si verifica un errore.  
  
 Se si utilizza il metodo [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) per ottenere informazioni sui parametri dal provider e vengono restituiti uno o più oggetti **parametro** di tipo di dati a lunghezza variabile, ADO può allocare memoria per i parametri in base alle dimensioni massime potenziali, che potrebbero causare un errore durante l'esecuzione. Per evitare un errore, è necessario impostare in modo esplicito la proprietà **size** per questi parametri prima di eseguire il comando.  
  
 La proprietà **size** è di lettura/scrittura.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Proprietà Size (Stream - ADO)](../../../ado/reference/ado-api/size-property-ado-stream.md)
