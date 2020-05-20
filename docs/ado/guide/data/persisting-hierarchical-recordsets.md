---
title: Salvataggio permanente di recordset gerarchici | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9c671adb19bd2e955b67ce23f268738ccf9033f5
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763122"
---
# <a name="persisting-hierarchical-recordsets"></a>Persistenza dei recordset gerarchici
È possibile salvare un **Recordset** gerarchico in un file in formato ADTG o XML chiamando il metodo [Save](../../../ado/reference/ado-api/save-method.md) . Tuttavia, quando si salva un **Recordset**gerarchico in formato XML si applicano due limitazioni: non è possibile salvare in XML se il **Recordset** gerarchico contiene aggiornamenti in sospeso e non è possibile salvare un **Recordset**gerarchico con parametri.  
  
 Per ulteriori informazioni sul provider data shaping, vedere [Microsoft Data Shaping Service for OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) e [Panoramica del servizio data shaping per OLE DB](https://msdn.microsoft.com/9f51e471-8e85-448e-9fb8-b64bbf767bf3).  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Grammatica forma formale](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)
