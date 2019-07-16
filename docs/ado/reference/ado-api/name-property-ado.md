---
title: Assegnare un nome proprietà (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a919bb377eee2da1c3c1a65e85ddfb9807ed8d50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918029"
---
# <a name="name-property-ado"></a>Proprietà Name (ADO)
Indica il nome di un oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** valore che indica il nome di un oggetto.  
  
## <a name="remarks"></a>Note  
 Usare la **nome** proprietà per assegnare un nome a o recuperare il nome di un **comando**, **proprietà**, **campo**, o **parametro**  oggetto.  
  
 Il valore è di lettura/scrittura in un **comandi** oggetto e sola lettura su un **proprietà** oggetto.  
  
 Per un **campo** oggetto **nome** viene in genere di sola lettura. Tuttavia, per ottenere nuove **campo** gli oggetti che sono stati accodati per il [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta di un [Record](../../../ado/reference/ado-api/record-object-ado.md), **nome** è lettura/scrittura solo dopo che il [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà per il **campo** è stato specificato e il provider di dati è stato aggiunto il nuovo **campo** chiamando il [ Update](../../../ado/reference/ado-api/update-method.md) metodo per il **campi** raccolta.  
  
 Per **parametri** gli oggetti non ancora aggiunto al [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) raccolta, il **nome** è di lettura/scrittura. Per aggiungere **parametri** gli oggetti e tutti gli altri oggetti, il **nome** proprietà è di sola lettura. I nomi non sono necessario essere univoco all'interno di una raccolta.  
  
 È possibile recuperare il **nome** proprietà di un oggetto per un riferimento ordinale, dopo il quale è possibile fare riferimento all'oggetto direttamente per nome. Ad esempio, se `rstMain.Properties(20).Name` produce `Updatability`, successivamente è possibile fare riferimento a questa proprietà come `rstMain.Properties("Updatability")`.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Oggetto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Name (VB) e attributi](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Esempio di proprietà Name (VC + +) e attributi](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
