---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b150fe1c0c7260960140558eeff74b54c0798d80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308622"
---
# <a name="createparameter-method-ado"></a>Metodo CreateParameter (ADO)
Crea un nuovo [parametro](../../../ado/reference/ado-api/parameter-object.md) oggetto con le proprietà specificate.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **parametro** oggetto.  
  
#### <a name="parameters"></a>Parametri  
 *Name*  
 Facoltativo. Un **stringa** che contiene il nome del valore il **parametro** oggetto.  
  
 *Tipo*  
 Facoltativo. Oggetto [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valore che specifica il tipo di dati di **parametro** oggetto.  
  
 *Direzione*  
 Facoltativo. Oggetto [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) che specifica il tipo di valore **parametro** oggetto.  
  
 *Dimensione*  
 Facoltativo. Oggetto **lungo** valore che specifica la lunghezza massima per il valore del parametro in caratteri o byte.  
  
 *Valore*  
 Facoltativo. Oggetto **Variant** che specifica il valore per il **parametro** oggetto.  
  
## <a name="remarks"></a>Note  
 Usare la **CreateParameter** per creare un nuovo metodo **parametro** oggetto con un nome specificato, tipo, direzione, dimensione e valore. Per il corrispondente vengono scritti i valori passati negli argomenti **parametro** proprietà.  
  
 Questo metodo non aggiunge automaticamente il **parametro** dell'oggetto per il **parametri** raccolta di un [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto. Ciò consente di impostare proprietà aggiuntive il cui ADO valori verrà convalidata quando si aggiunge il **parametro** oggetto alla raccolta.  
  
 Se si specifica un tipo di dati a lunghezza variabile nel *tipo* argomento, è necessario passare un *dimensioni* argomento o un set di [dimensioni](../../../ado/reference/ado-api/size-property-ado-parameter.md) proprietà del **parametro**  oggetto prima di accodare per il **parametri** insieme; in caso contrario, si verifica un errore.  
  
 Se si specifica un tipo di dati numerico (**adNumeric** oppure **adDecimal**) nel *tipo* argomento, sarà necessario impostare anche il [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) e [Precisione](../../../ado/reference/ado-api/precision-property-ado.md) proprietà.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Append e CreateParameter (esempio di metodi (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append e CreateParameter metodi (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Metodo Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)   
 [Raccolta di parametri (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
