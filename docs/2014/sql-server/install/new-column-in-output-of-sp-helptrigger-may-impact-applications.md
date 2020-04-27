---
title: La nuova colonna nell'output di sp_helptrigger può influisca sulle applicazioni | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093743"
---
# <a name="new-column-in-output-of-sp_helptrigger-may-impact-applications"></a>La nuova colonna nell'output di sp_helptrigger potrebbe influire sulle applicazioni
  trigger_schemaias l'ultima colonna del set di risultati restituito dalla stored procedure di sistema di sp_helptrigger.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Per ottenere informazioni sui trigger definiti in una specifica tabella, eseguire una query sulla vista del catalogo sys.triggers.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
 Esaminare l'utilizzo di sp_helptrigger nelle applicazioni. Può essere necessario modificare le applicazioni in modo da gestire la colonna aggiuntiva. In alternativa, è possibile utilizzare la vista del catalogo sys. Triggers.  
  
## <a name="see-also"></a>Vedi anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
