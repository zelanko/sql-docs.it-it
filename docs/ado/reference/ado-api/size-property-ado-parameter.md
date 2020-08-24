---
description: Proprietà Size (Parameter - ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2bede13c00304565a0e3b7819be7c8e6a5b5ca48
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777480"
---
# <a name="size-property-ado-parameter"></a>Proprietà Size (Parameter - ADO)
Indica la dimensione massima, in byte o caratteri, di un oggetto [Parameter](./parameter-object.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** che indica la dimensione massima in byte o caratteri di un valore in un oggetto **Parameter** .  
  
## <a name="remarks"></a>Commenti  
 Utilizzare la proprietà **size** per determinare le dimensioni massime per i valori scritti o letti dalla proprietà [value](./value-property-ado.md) di un oggetto **Parameter** .  
  
 Se si specifica un tipo di dati a lunghezza variabile per un oggetto **Parameter** (ad esempio, qualsiasi tipo **stringa** , ad esempio **adVarChar**), è necessario impostare la proprietà **size** dell'oggetto prima di aggiungerlo alla raccolta [Parameters](./parameters-collection-ado.md) . in caso contrario, si verifica un errore.  
  
 Se è già stato aggiunto l'oggetto **Parameter** alla raccolta **Parameters** di un oggetto [Command](./command-object-ado.md) e il tipo viene modificato in un tipo di dati a lunghezza variabile, è necessario impostare la proprietà **size** dell'oggetto **Parameter** prima di eseguire l'oggetto **Command** . in caso contrario, si verifica un errore.  
  
 Se si utilizza il metodo [Refresh](./refresh-method-ado.md) per ottenere informazioni sui parametri dal provider e vengono restituiti uno o più oggetti **parametro** di tipo di dati a lunghezza variabile, ADO può allocare memoria per i parametri in base alle dimensioni massime potenziali, che potrebbero causare un errore durante l'esecuzione. Per evitare un errore, è necessario impostare in modo esplicito la proprietà **size** per questi parametri prima di eseguire il comando.  
  
 La proprietà **size** è di lettura/scrittura.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Parameter](./parameter-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Proprietà Size (Stream - ADO)](./size-property-ado-stream.md)