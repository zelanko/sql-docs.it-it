---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac5097a8692ed7a9e6566707354112547c5a619c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864012"
---
# <a name="maxrecords-property-ado"></a>Proprietà MaxRecords (ADO)
Indica il numero massimo di record da restituire per una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) da una query.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **lungo** valore che indica il numero massimo di record da restituire. Valore predefinito è zero (**0**), che indica nessun limite.  
  
## <a name="remarks"></a>Note  
 Usare la **MaxRecords** proprietà per limitare il numero di record che restituisce il provider dell'origine dati. L'impostazione predefinita di questa proprietà è zero, ovvero che il provider restituisce che tutti i record richiesti.  
  
 Il **MaxRecords** è di lettura/scrittura quando il **Recordset** viene chiuso e di sola lettura quando è aperta.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà MaxRecords (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [Esempio di proprietà MaxRecords (VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
