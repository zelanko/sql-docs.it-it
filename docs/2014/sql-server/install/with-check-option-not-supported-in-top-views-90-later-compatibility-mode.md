---
title: WITH CHECK OPTION non è supportata nelle viste che contengono TOP in modalità di compatibilità 90 o successive | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- TOP clause
- WITH CHECK OPTION clause
ms.assetid: 1b9581d0-bad9-43e0-b8fc-f32d8a8a04ca
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 254969e6201795e2f4ae512e03be26419b71d866
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66090994"
---
# <a name="with-check-option-is-not-supported-in-views-that-contain-top-in-90-or-later-compatibility-modes"></a>WITH CHECK OPTION non è supportata nelle viste che contengono TOP nella modalità di compatibilità 90 o successiva
  È presente una vista definita utilizzando la clausola WITH CHECK OPTION e una clausola TOP nell'istruzione SELECT della vista o in una vista a cui fa riferimento. In modalità di compatibilità del database 80 e precedenti, le viste definite in questo modo consentono la modifica dei dati tramite la vista. Questo comportamento non è corretto e può dare luogo a risultati non accurati. I dati non possono essere inseriti o aggiornati tramite una vista che utilizza una clausola WITH CHECK OPTION se tale vista o una vista a cui fa riferimento utilizza la clausola TOP e la modalità di compatibilità del database è 90 o successiva.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Quando si esegue l'aggiornamento, la modalità di compatibilità dei database utente non cambia. Prima di impostare la modalità di compatibilità del database su 100 o successiva, modificare le viste che utilizzano le clausole WITH CHECK OPTION e TOP se è richiesta la modifica di dati tramite la vista. Per ulteriori informazioni, vedere [sp_dbcmptlevel &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-dbcmptlevel-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
