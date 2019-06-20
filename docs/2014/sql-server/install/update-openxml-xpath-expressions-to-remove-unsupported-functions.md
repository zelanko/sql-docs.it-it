---
title: Aggiornare le espressioni XPath OPENXML per rimuovere le funzioni non supportate | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- OPENXML queries
ms.assetid: b459abaf-8787-4b65-9231-ae30e5469fd0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec0edb2e72143fd41709355a3e9cc338544289a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091689"
---
# <a name="update-openxml-xpath-expressions-to-remove-unsupported-functions"></a>Aggiornare le espressioni XPath OPENXML in modo da rimuovere le funzioni non supportate
  È stata rilevata la funzionalità XPath. Dopo l'aggiornamento è possibile che le modifiche alla funzionalità XPath abbiano effetto per le funzionalità OPENXML.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 MSXML 3.0 è il motore sottostante utilizzato per l'elaborazione di espressioni XPath incluse in query OPENXML. MSXML 3.0 include un motore XPath 1.0 più restrittivo che non supporta più le funzioni seguenti:  
  
-   format-number()  
  
-   formatNumber()  
  
-   current()  
  
-   element-available()  
  
-   function-available()  
  
-   system-property()  
  
## <a name="corrective-action"></a>Azione correttiva  
 Nel caso di format-number() e formatNumber(), è possibile utilizzare [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per le altre funzioni non supportate elencate in precedenza, non sono disponibili soluzioni alternative dirette.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
