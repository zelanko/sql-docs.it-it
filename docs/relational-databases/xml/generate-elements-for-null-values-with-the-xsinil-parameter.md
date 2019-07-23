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
ms.openlocfilehash: 2373da54981ad8d3cc743214c7110bb0d49723bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943147"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>Generazione di elementi per valori NULL tramite il parametro XSINIL

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

La direttiva **ELEMENTS** costruisce codice XML nel quale viene eseguito il mapping di ogni valore di colonna a un elemento. Per impostazione predefinita, se il valore di colonna è NULL, non viene aggiunto alcun elemento. Ma specificando il parametro facoltativo **XSINIL** nella direttiva ELEMENTS, è possibile richiedere che venga creato un elemento anche per il valore NULL. In questo caso, per ogni valore di colonna NULL viene restituito un elemento con l'attributo **xsi:nil** impostato su TRUE.  
  
## <a name="see-also"></a>Vedere anche

[Usare la modalità RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)

[Clausola SELECT - FOR](../../t-sql/queries/select-for-clause-transact-sql.md)
