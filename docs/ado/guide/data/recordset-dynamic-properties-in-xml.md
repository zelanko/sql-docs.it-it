---
description: Proprietà dinamiche dei recordset in XML
title: Proprietà dinamiche del recordset in XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: rothja
ms.author: jroth
ms.openlocfilehash: 395a81108e3ceaed99ad8ccf1fbab29831dd116d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979892"
---
# <a name="recordset-dynamic-properties-in-xml"></a>Proprietà dinamiche dei recordset in XML
Le seguenti proprietà specifiche del provider recordset (dal motore di cursore client) sono attualmente rese permanente nel formato XML:  
  
-   Aggiornamento della risincronizzazione  
  
-   tabella univoca  
  
-   Schema univoco  
  
-   Catalogo univoco  
  
-   Comando di risincronizzazione  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Nome riforma  
  
-   AutoRecalc  
  
 Queste proprietà vengono salvate nella sezione dello schema come attributi della definizione dell'elemento per il recordset da salvare in modo permanente. Questi attributi sono definiti nello spazio dei nomi dello schema del set di righe e devono avere il prefisso "RS:".  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
