---
description: Proprietà PageSize (ADO)
title: Proprietà PageSize (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageSize
helpviewer_keywords:
- PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
author: rothja
ms.author: jroth
ms.openlocfilehash: 99365747e5049da4b8dd3cc58f58fd6e2a542e76
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442853"
---
# <a name="pagesize-property-ado"></a>Proprietà PageSize (ADO)
Indica il numero di record che costituiscono una pagina nel [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** che indica il numero di record presenti in una pagina. Il valore predefinito è **10**.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **pageSize** per determinare il numero di record che costituiscono una pagina logica di dati. La definizione di una dimensione di pagina consente di usare la proprietà [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) per passare al primo record di una pagina specifica. Questa operazione è utile negli scenari server Web quando si desidera consentire all'utente di eseguire il paging dei dati, visualizzando un determinato numero di record alla volta.  
  
 Questa proprietà può essere impostata in qualsiasi momento e il relativo valore verrà usato per calcolare la posizione del primo record di una pagina specifica.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà AbsolutePage, PageCount e PageSize (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [Esempio di proprietà AbsolutePage, PageCount e PageSize (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Proprietà AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Proprietà PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
