---
description: Proprietà MaxRecords (ADO)
title: Proprietà MaxRecords (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
author: rothja
ms.author: jroth
ms.openlocfilehash: 4431d9a8af8623150717474cd5429a772f86be8c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774450"
---
# <a name="maxrecords-property-ado"></a>Proprietà MaxRecords (ADO)
Indica il numero massimo di record da restituire a un [Recordset](./recordset-object-ado.md) da una query.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** che indica il numero massimo di record da restituire. Il valore predefinito è zero (**0**), che indica nessun limite.  
  
## <a name="remarks"></a>Commenti  
 Utilizzare la proprietà **maxRecords** per limitare il numero di record restituiti dal provider dall'origine dati. L'impostazione predefinita di questa proprietà è zero, il che significa che il provider restituisce tutti i record richiesti.  
  
 La proprietà **maxRecords** è in lettura/scrittura quando il **Recordset** è chiuso e in sola lettura quando è aperto.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà MaxRecords (VB)](./maxrecords-property-example-vb.md)   
 [Esempio della proprietà MaxRecords (VC++)](./maxrecords-property-example-vc.md)