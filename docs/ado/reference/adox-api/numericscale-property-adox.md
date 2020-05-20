---
title: Proprietà NumericScale (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::PutNumericScale
- _Column::GetNumericScale
- _Column::NumericScale
- _Column::put_NumericScale
- _Column::get_NumericScale
helpviewer_keywords:
- NumericScale property [ADOX]
ms.assetid: 573ee5d1-57c7-4a27-be79-a0e12944ad9b
author: rothja
ms.author: jroth
ms.openlocfilehash: a0a0090a24207e6faad1b14aa3cb5afd6091bc87
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763812"
---
# <a name="numericscale-property-adox"></a>Proprietà NumericScale (ADOX)
Indica la scala di un valore numerico nella colonna.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta e restituisce un valore **byte** che rappresenta la scala dei valori di dati nella colonna quando la proprietà [Type](../../../ado/reference/adox-api/type-property-column-adox.md) è **adNumeric** o **adDecimal**. **NumericScale** viene ignorato per tutti gli altri tipi di dati.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore predefinito è zero (0).  
  
 **NumericScale** è di sola lettura per gli oggetti [Column](../../../ado/reference/adox-api/column-object-adox.md) già accodati a una raccolta.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di codice ADOX: esempio di proprietà NumericScale e Precision (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Proprietà Type (Column) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
