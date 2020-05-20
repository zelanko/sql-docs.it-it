---
title: Proprietà Precision (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::put_Precision
- _Column::PutPrecision
- _Column::GetPrecision
- _Column::get_Precision
- _Column::Precision
helpviewer_keywords:
- Precision property [ADOX]
ms.assetid: 0e0ecbbf-d7de-49d4-a128-5a519ecd54ba
author: rothja
ms.author: jroth
ms.openlocfilehash: 67512b74e4c2b869cb7b1f9397462ce5566557a8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763722"
---
# <a name="precision-property-adox"></a>Proprietà Precision (ADOX)
Indica la precisione massima dei valori dei dati nella [colonna](../../../ado/reference/adox-api/column-object-adox.md).  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta e restituisce un valore **Long** che rappresenta la precisione massima dei valori dei dati nella colonna quando la proprietà [Type](../../../ado/reference/adox-api/type-property-column-adox.md) è di tipo numerico. La **precisione** viene ignorata per tutti gli altri tipi di dati.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore predefinito è zero (**0**).  
  
 Questa proprietà è di sola lettura per gli oggetti [Column](../../../ado/reference/adox-api/column-object-adox.md) già accodati a una raccolta.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di codice ADOX: esempio di proprietà NumericScale e Precision (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Proprietà Type (Column) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)   
 [Oggetto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
