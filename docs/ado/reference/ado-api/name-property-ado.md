---
title: Proprietà Name (ADO) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918029"
---
# <a name="name-property-ado"></a>Proprietà Name (ADO)
Indica il nome di un oggetto.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **stringa** che indica il nome di un oggetto.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **Name** per assegnare un nome a o recuperare il nome di un **comando**, di una **proprietà**, di un **campo**o di un oggetto **Parameter** .  
  
 Il valore è in lettura/scrittura su un oggetto **Command** e in sola lettura su un oggetto **Property** .  
  
 Per un oggetto **campo** , il **nome** è in genere di sola lettura. Tuttavia, per i nuovi oggetti **campo** aggiunti alla raccolta [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) di un [record](../../../ado/reference/ado-api/record-object-ado.md), il **nome** è di lettura/scrittura solo dopo che è stata specificata la proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) per il **campo** e il provider di dati ha aggiunto correttamente il nuovo **campo** chiamando il metodo [Update](../../../ado/reference/ado-api/update-method.md) della raccolta **Fields** .  
  
 Per gli oggetti **Parameter** non ancora aggiunti alla raccolta [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) , la proprietà **Name** è di lettura/scrittura. Per gli oggetti **parametro** accodati e per tutti gli altri oggetti, la proprietà **Name** è di sola lettura. Non è necessario che i nomi siano univoci all'interno di una raccolta.  
  
 È possibile recuperare la proprietà **Name** di un oggetto in base a un riferimento ordinale, dopo di che è possibile fare riferimento all'oggetto direttamente in base al nome. Se `rstMain.Properties(20).Name` , ad esempio, restituisce `Updatability`, è possibile fare riferimento a questa proprietà come `rstMain.Properties("Updatability")`.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Oggetto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Vedi anche  
 [Esempio di proprietà Attributes e Name (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Esempio di proprietà Attributes e Name (VC + +)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
