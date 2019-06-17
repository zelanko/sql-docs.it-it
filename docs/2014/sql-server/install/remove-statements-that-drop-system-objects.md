---
title: Rimuovere le istruzioni che eliminano oggetti di sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d420e2dba1dfdb284b0002eca6d8408c4e019e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093081"
---
# <a name="remove-statements-that-drop-system-objects"></a>Rimuovere le istruzioni che eliminano oggetti di sistema
  Sono state rilevate istruzioni che eliminano oggetti di sistema. Gli oggetti di sistema, incluse le stored procedure estese, vengono distribuiti in sola lettura **risorsa** (mssqlsystemresource) del database e non può essere eliminata. Modificare le applicazioni in modo da revocare o negare l'autorizzazione EXECUTE sugli oggetti di sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Istruzioni quali DROP TABLE, DROP PROCEDURE e **sp_dropextendedproc** non può essere utilizzato per rimuovere gli oggetti di sistema, poiché questi oggetti vengono distribuiti in sola lettura **risorsa** database.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Rimuovere dalle applicazioni tutte le istruzioni che tentano di eliminare oggetti di sistema. Modificare le applicazioni in modo da revocare o negare l'autorizzazione EXECUTE sugli oggetti di sistema. In alternativa è possibile utilizzare uno degli strumenti Configurazione superficie di attacco per disabilitare alcuni di questi oggetti. Ad esempio, il **xp_cmdshell** stored procedure estesa può essere disabilitata o attivata tramite lo strumento Configurazione superficie di attacco.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
