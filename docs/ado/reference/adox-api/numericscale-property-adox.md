---
description: Proprietà NumericScale (ADOX)
title: Proprietà NumericScale (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 161b6049ca5392eafacaf0fd97db653070f105e0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983892"
---
# <a name="numericscale-property-adox"></a>Proprietà NumericScale (ADOX)
Indica la scala di un valore numerico nella colonna.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta e restituisce un valore **byte** che rappresenta la scala dei valori di dati nella colonna quando la proprietà [Type](./type-property-column-adox.md) è **adNumeric** o **adDecimal**. **NumericScale** viene ignorato per tutti gli altri tipi di dati.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore predefinito è zero (0).  
  
 **NumericScale** è di sola lettura per gli oggetti [Column](./column-object-adox.md) già accodati a una raccolta.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Column (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di codice ADOX: esempio di proprietà NumericScale e Precision (VB)](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Proprietà Type (Column) (ADOX)](./type-property-column-adox.md)