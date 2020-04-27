---
title: Visualizzare le destinazioni degli eventi estesi per i pacchetti registrati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events]
- viewing event targets
- extended events [SQL Server], viewing targets
ms.assetid: 4985aa5f-ac99-49f6-852c-9d25916549e9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ae927a281db54697bbda49e28a58ea4c6e60326a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088725"
---
# <a name="view-the-extended-events-targets-for-registered-packages"></a>Visualizzare le destinazioni degli eventi estesi per i pacchetti registrati
  Prima di creare una sessione Eventi estesi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è utile determinare le destinazioni degli eventi estesi disponibili. Questa attività comporta l'utilizzo dell'editor di query in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per eseguire la procedura descritta di seguito.  
  
 Dopo aver eseguito le istruzioni di questa procedura, nella scheda **Risultati** dell'editor di query vengono visualizzate le due colonne seguenti:  
  
-   package_name  
  
-   target_name  
  
## <a name="to-view-the-extended-events-targets-for-registered-packages-using-query-editor"></a>Per visualizzare le destinazioni di Eventi estesi per i pacchetti registrati utilizzando l'editor di query  
  
-   Nell'editor di query eseguire le istruzioni indicate di seguito.  
  
    ```  
    USE msdb  
    SELECT p.name package_name, o.name target_name  
    FROM sys.dm_xe_objects o  
    JOIN sys.dm_xe_packages p  
         ON o.package_guid = p.guid  
    WHERE o.object_type = 'target'  
    ```  
  
## <a name="see-also"></a>Vedi anche  
 [SQL Server destinazioni degli eventi estesi](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys. dm_xe_objects &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
