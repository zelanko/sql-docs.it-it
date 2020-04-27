---
title: Usare sp_rename per rinominare il nome di indice duplicato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- table names [SQL Server]
- duplicate table names
- index names [SQL Server]
- sp_rename
- duplicate index names
ms.assetid: ee66c7a5-eb6d-4fcf-970c-ab099d78c8d9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3ca4efb2a16f615af57e89fa56a4dcb8bdb3bf5d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091363"
---
# <a name="use-sp_rename-to-rename-duplicate-index-name"></a>Utilizzare sp_rename per rinominare gli indici duplicati
  Sono stati rilevati nomi di indici di tabella o di vista duplicati. Rinominare gli indici prima di eseguire l'aggiornamento.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Azione correttiva  
  
1.  Individuare gli indici duplicati eseguendo la query seguente:  
  
    ```  
    SELECT DISTINCT OBJECT_NAME(o.id), name  
    FROM sysindexes as o  
    WHERE EXISTS   
        (SELECT name FROM sysindexes  as i  
          WHERE i.id = o.id  
          AND i.name = o.name and i.indid < o.indid);  
    ```  
  
2.  Utilizzare **sp_rename** per modificare uno dei nomi degli indici. Poiché i nomi di indice sono uguali, non è possibile determinare quale indice verrà rinominato. Questa operazione consente quindi di differenziare gli indici.  
  
    ```  
    EXEC sp_rename N'table_name.index_name', N'new_index_name', N'INDEX'  
    ```  
  
3.  Per verificare quale indice è stato rinominato eseguire la query seguente, che restituisce tutti gli indici, inclusi i nomi delle colonne chiave sulla tabella o vista specificata:  
  
    ```  
    SELECT i.name AS IndexName, c.name AS ColumnName, ik.colid, ik.keyno  
    FROM sysindexes i  
    JOIN sysindexkeys ik ON i.id = ik.id and i.indid = ik.indid   
    JOIN syscolumns c ON c.id = ik.id and ik.colid = c.colid  
    WHERE i.id = OBJECT_ID('table_or_view_name')  
    ```  
  
4.  Se necessario, utilizzare di nuovo **sp_rename** per correggere i nomi degli indici.  
  
## <a name="see-also"></a>Vedi anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
