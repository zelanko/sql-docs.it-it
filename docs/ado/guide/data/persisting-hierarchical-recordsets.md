---
title: Persistenza di recordset gerarchici | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f25b61ca54b3a4ac15584ecf31874f90787c735d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700464"
---
# <a name="persisting-hierarchical-recordsets"></a>Persistenza dei recordset gerarchici
È possibile salvare un modello gerarchico **Recordset** in un file in formato ADTG o XML chiamando la [salvare](../../../ado/reference/ado-api/save-method.md) (metodo). Tuttavia, due limitazioni si applicano durante il salvataggio gerarchica **Recordset**s in formato XML: Se non è possibile salvare in XML la gerarchica **Recordset** include aggiornamenti, in sospeso e non è possibile salvare un con parametri gerarchici **Recordset**.  
  
 Per altre informazioni sul provider di Data Shaping, vedere [Microsoft Data shaping per OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) e [Panoramica del servizio Data Shaping dei dati per OLE DB](https://msdn.microsoft.com/9f51e471-8e85-448e-9fb8-b64bbf767bf3).  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Grammatica formale per Shape](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)
