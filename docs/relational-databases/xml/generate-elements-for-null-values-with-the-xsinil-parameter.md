---
title: Generare elementi per valori NULL tramite il parametro XSINIL | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0889de0a7525e0e5a7ea91ba169011aaf4e341a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175181"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>Generazione di elementi per valori NULL tramite il parametro XSINIL

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

La direttiva **ELEMENTS** costruisce codice XML nel quale viene eseguito il mapping di ogni valore di colonna a un elemento. Per impostazione predefinita, se il valore di colonna è NULL, non viene aggiunto alcun elemento. Ma specificando il parametro facoltativo **XSINIL** nella direttiva ELEMENTS, è possibile richiedere che venga creato un elemento anche per il valore NULL. In questo caso, per ogni valore di colonna NULL viene restituito un elemento con l'attributo **xsi:nil** impostato su TRUE.  
  
## <a name="see-also"></a>Vedere anche

[Usare la modalità RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)

[Clausola SELECT - FOR](../../t-sql/queries/select-for-clause-transact-sql.md)
