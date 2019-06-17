---
title: CursorLocationEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 43c2043917d6b21293fea71566dfdf1202b6f59e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695658"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
Specifica la posizione del servizio di cursore.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|Utilizza i cursori sul lato client forniti da una libreria di cursori locali. Il cursore locale services spesso consentirà molte funzionalità che i cursori fornito dal driver, non possono pertanto usare questa impostazione può offrire un vantaggio rispetto alla funzionalità che verranno abilitati. Per la compatibilità con le versioni precedenti, il sinonimo **adUseClientBatch** è anche supportato.|  
|**adUseNone**|1|Non utilizzare servizi di cursore. (Questa costante è obsoleta e viene visualizzato unicamente per compatibilità con le versioni precedenti).|  
|**adUseServer**|2|Valore predefinito. Utilizza i cursori forniti dal provider di dati o driver. Questi cursori sono a volte è molto flessibili e consentano aggiuntive sensibilità alle modifiche apportate da altri file di dati. Tuttavia, alcune funzionalità dei [The Microsoft Cursor Service per OLE DB](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md), ad esempio rimossa l'associazione<br /><br /> [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetti, non possono essere simulati con cursori sul lato server e queste funzionalità non sarà disponibile con questa impostazione.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
