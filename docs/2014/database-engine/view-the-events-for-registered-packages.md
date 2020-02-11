---
title: Visualizzare gli eventi per i pacchetti registrati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- viewing events
- extended events [SQL Server], viewing events
ms.assetid: 9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1156a7272edc8ad1ecfb8e173f81bc678800c855
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089624"
---
# <a name="view-the-events-for-registered-packages"></a>Visualizzare gli eventi per i pacchetti registrati
  Prima di creare una sessione degli eventi estesi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , è utile individuare gli eventi disponibili nei pacchetti registrati. Per ulteriori informazioni, vedere [SQL Server Extended Events Packages](../relational-databases/extended-events/sql-server-extended-events-packages.md).  
  
 Il completamento di questa attività comporta l'utilizzo dell'editor di query in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per effettuare la procedura descritta di seguito.  
  
 Al termine delle istruzioni in questa procedura, nella scheda **Risultati** dell'editor di query vengono visualizzate le seguenti colonne:  
  
-   name. Nome del pacchetto.  
  
-   event. Nome dell'evento.  
  
-   keyword. Parola chiave derivata da una tabella di mapping numerica interna.  
  
-   channel. Gruppo di destinatari per un evento.  
  
-   description. Descrizione dell'evento.  
  
## <a name="to-view-the-events-for-registered-packages-using-query-editor"></a>Per visualizzare gli eventi per i pacchetti registrati utilizzando l'editor di query  
  
-   Nell'editor di query eseguire le istruzioni indicate di seguito.  
  
    ```  
    USE msdb  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
    (  
    SELECT event_package=o.package_guid, o.description,   
    event=c.object_name, channel=v.map_value  
    FROM sys.dm_xe_objects o  
    LEFT JOIN sys.dm_xe_object_columns c ON o.name=c.object_name  
    INNER JOIN sys.dm_xe_map_values v ON c.type_name=v.name   
    AND c.column_value=cast(v.map_key AS nvarchar)  
    WHERE object_type='event' AND (c.name='CHANNEL' or c.name IS NULL)  
  
    ) c LEFT JOIN   
    (  
    SELECT event_package=c.object_package_guid, event=c.object_name,   
    keyword=v.map_value  
    FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
    ON c.type_name=v.name AND c.column_value=v.map_key   
    AND c.type_package_guid=v.object_package_guid  
    INNER JOIN sys.dm_xe_objects o ON o.name=c.object_name   
    AND o.package_guid=c.object_package_guid  
    WHERE object_type='event' AND c.name='KEYWORD'   
    ) k  
    ON  
    k.event_package=c.event_package AND (k.event=c.event or k.event IS NULL)  
    INNER JOIN sys.dm_xe_packages p ON p.guid=c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server pacchetti di eventi estesi](../relational-databases/extended-events/sql-server-extended-events-packages.md)   
 [sys. dm_xe_objects &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
