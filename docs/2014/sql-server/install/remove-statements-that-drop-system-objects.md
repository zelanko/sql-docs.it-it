---
title: Rimuovere le istruzioni che eliminano oggetti di sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68e5000e924c438a4611e2fa8c134f0dd822f930
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294486"
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
  
  
