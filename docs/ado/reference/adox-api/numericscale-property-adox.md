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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ba72974f9531d328a40244d4ec4ee736ab162fa0
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706262"
---
# <a name="numericscale-property-adox"></a>Proprietà NumericScale (ADOX)
Indica la scala di un valore numerico nella colonna.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta e restituisce un **Byte** valore che rappresenta la scala dei valori dei dati nella colonna quando il [tipo](../../../ado/reference/adox-api/type-property-column-adox.md) proprietà è **adNumeric** oppure **adDecimal**. **NumericScale** viene ignorato per tutti gli altri tipi di dati.  
  
## <a name="remarks"></a>Note  
 Il valore predefinito è zero (0).  
  
 **NumericScale** è di sola lettura per [colonna](../../../ado/reference/adox-api/column-object-adox.md) già aggiunti a una raccolta di oggetti.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di codice: Esempio NumericScale e Precision Properties (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Proprietà Type (Column) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
