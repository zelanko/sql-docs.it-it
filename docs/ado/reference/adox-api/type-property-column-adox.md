---
description: Proprietà Type (Column) (ADOX)
title: Proprietà Type (Column) (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::Type
- _Column::GetType
- _Column::get_Type
- _Column::put_Type
- _Column::PutType
helpviewer_keywords:
- Type property [ADOX]
ms.assetid: 5c6718b6-f728-478a-8afb-5d17b0a91d1f
author: rothja
ms.author: jroth
ms.openlocfilehash: 70d8700f953a87fa3326f6a1c0985be1f6ca3dac
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769220"
---
# <a name="type-property-column-adox"></a>Proprietà Type (Column) (ADOX)
Indica il tipo di dati di una colonna.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** che può essere una delle costanti [DataTypeEnum](../ado-api/datatypeenum.md) . Il valore predefinito è **adVarWChar**.  
  
## <a name="remarks"></a>Commenti  
 Questa proprietà è di lettura/scrittura finché l'oggetto [colonna](./column-object-adox.md) non viene accodato a una raccolta o a un altro oggetto, dopo il quale è di sola lettura.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Column (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Proprietà Type (Key) (ADOX)](./type-property-key-adox.md)   
 [Proprietà Type (Table) (ADOX)](./type-property-table-adox.md)