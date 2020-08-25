---
description: Proprietà Attributes (ADOX)
title: Proprietà Attributes (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::put_Attributes
- _Column::Attributes
- _Column::PutAttributes
- _Column::get_Attributes
- _Column::GetAttributes
helpviewer_keywords:
- Attributes property [ADOX]
ms.assetid: e3abb359-79a3-4c22-b3a8-2900817e0d23
author: rothja
ms.author: jroth
ms.openlocfilehash: b2fca7e2cf9bce25d1993d16d4ec6a44bf53ef67
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771350"
---
# <a name="attributes-property-adox"></a>Proprietà Attributes (ADOX)
Descrive le caratteristiche della colonna.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** . Il valore specifica le caratteristiche della tabella rappresentata dall'oggetto [colonna](./column-object-adox.md) . Il valore può essere una combinazione di costanti [ColumnAttributesEnum](./columnattributesenum.md) . Il valore predefinito è zero (**0**), che non è né **adColFixed** né **adColNullable**.  
  
## <a name="applies-to"></a>Si applica a  
  
- [Oggetto Column (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio della proprietà Attributes (VB)](./attributes-property-example-vb.md)