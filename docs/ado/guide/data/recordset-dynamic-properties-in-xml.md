---
title: Proprietà dinamiche del recordset in formato XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a058a2d0c5a808f29807744c6ba01f658bebc120
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924441"
---
# <a name="recordset-dynamic-properties-in-xml"></a>Proprietà dinamiche dei recordset in XML
Le seguenti proprietà specifiche del provider di Recordset (dal motore del cursore Client) vengono attualmente mantenute in formato XML:  
  
-   Update Resync  
  
-   tabella univoca  
  
-   Schema univoco  
  
-   Catalogo univoco  
  
-   La risincronizzazione di comando  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Proprietà dinamica Reshape Name  
  
-   AutoRecalc  
  
 Queste proprietà vengono salvate nella sezione schema come attributi di definizione dell'elemento per il Recordset vengano resi persistente. Questi attributi sono definiti nello spazio dei nomi dello schema del set di righe e deve avere il prefisso "rs:".  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
