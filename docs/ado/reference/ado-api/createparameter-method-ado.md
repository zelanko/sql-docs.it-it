---
description: Metodo CreateParameter (ADO)
title: Metodo CreateParameter (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6bf45e2d458784972d7057e95878c9db3526ffac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444323"
---
# <a name="createparameter-method-ado"></a>Metodo CreateParameter (ADO)
Crea un nuovo oggetto [Parameter](../../../ado/reference/ado-api/parameter-object.md) con le proprietà specificate.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un oggetto **Parameter** .  
  
#### <a name="parameters"></a>Parametri  
 *Nome*  
 Facoltativo. Valore **stringa** che contiene il nome dell'oggetto **Parameter** .  
  
 *Tipo*  
 Facoltativo. Valore [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) che specifica il tipo di dati dell'oggetto **Parameter** .  
  
 *Direzione*  
 Facoltativo. Valore [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) che specifica il tipo di oggetto **Parameter** .  
  
 *Dimensione*  
 Facoltativo. Valore **Long** che specifica la lunghezza massima del valore del parametro in caratteri o byte.  
  
 *Valore*  
 Facoltativo. **Variant** che specifica il valore per l'oggetto **Parameter** .  
  
## <a name="remarks"></a>Osservazioni  
 Usare il metodo **CreateParameter** per creare un nuovo oggetto **Parameter** con un nome, un tipo, una direzione, una dimensione e un valore specificati. Tutti i valori passati negli argomenti vengono scritti nelle proprietà dei **parametri** corrispondenti.  
  
 Questo metodo non aggiunge automaticamente l'oggetto **Parameter** alla raccolta **Parameters** di un oggetto [Command](../../../ado/reference/ado-api/command-object-ado.md) . Ciò consente di impostare proprietà aggiuntive i cui valori ADO verranno convalidati quando si aggiunge l'oggetto **Parameter** alla raccolta.  
  
 Se si specifica un tipo di dati a lunghezza variabile nell'argomento *tipo* , è necessario passare un argomento *size* o impostare la proprietà [size](../../../ado/reference/ado-api/size-property-ado-parameter.md) dell'oggetto **Parameter** prima di accodarlo alla raccolta **Parameters** . in caso contrario, si verifica un errore.  
  
 Se si specifica un tipo di dati numerico (**adNumeric** o **adDecimal**) nell'argomento *tipo* , è necessario impostare anche le proprietà [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) e [Precision](../../../ado/reference/ado-api/precision-property-ado.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi Append e CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Esempio di metodi Append e CreateParameter (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Metodo Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Parameter (oggetto)](../../../ado/reference/ado-api/parameter-object.md)   
 [Raccolta Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
