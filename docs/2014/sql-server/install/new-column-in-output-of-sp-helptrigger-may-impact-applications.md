---
title: La nuova colonna nell'output di sp_helptrigger potrebbe influire sulle applicazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sp_helptrigger
ms.assetid: b7c42a8f-f2e0-4fa3-b046-3cf39c854c47
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 33d47c858a03766260e8ed8c098fef79e9e4a82f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66093743"
---
# <a name="new-column-in-output-of-sphelptrigger-may-impact-applications"></a>La nuova colonna nell'output di sp_helptrigger potrebbe influire sulle applicazioni
  l'ultima colonna nel set di risultati restituita dal sistema sp_helptrigger trigger_schemaias di stored procedure.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Per ottenere informazioni sui trigger definiti in una specifica tabella, eseguire una query sulla vista del catalogo sys.triggers.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Esaminare l'utilizzo di sp_helptrigger nelle applicazioni. Può essere necessario modificare le applicazioni in modo da gestire la colonna aggiuntiva. In alternativa, è possibile utilizzare invece la vista del catalogo sys. Triggers.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
