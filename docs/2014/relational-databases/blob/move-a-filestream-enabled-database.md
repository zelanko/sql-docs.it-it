---
title: Spostare un database abilitato per FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], moving a FILESTREAM-enabled database
ms.assetid: dd4d270d-9283-431a-aa6b-e571fced1893
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aaf6dffd3d8424f5582a43d327ce6f2b3e26af4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66009961"
---
# <a name="move-a-filestream-enabled-database"></a>Spostamento di un database abilitato per FILESTREAM
  In questo argomento viene illustrato come spostare un database abilitato per FILESTREAM.  
  
> [!NOTE]  
>  Gli esempi di questo argomento presuppongono l'uso del database Archive creato in [Creare un database abilitato per FILESTREAM](create-a-filestream-enabled-database.md).  
  
### <a name="to-move-a-filestream-enabled-database"></a>Per spostare un database abilitato per FILESTREAM  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic su **Nuova query** per aprire l'editor di query.  
  
2.  Copiare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente nell'editor di query e fare clic su **Esegui**. Lo script consentirà di visualizzare la posizione dei file fisici del database utilizzati dal database FILESTREAM.  
  
    ```sql  
    USE Archive  
    GO  
    SELECT type_desc, name, physical_name from sys.database_files  
    ```  
  
3.  Copiare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente nell'editor di query e fare clic su **Esegui**. Questo codice consente di attivare la modalità offline per il database `Archive` .  
  
    ```sql  
    USE master  
    EXEC sp_detach_db Archive  
    GO  
    ```  
  
4.  Creare la cartella `C:\moved_location`, quindi spostarvi i file e le cartelle elencati nel passaggio 2.  
  
5.  Copiare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente nell'editor di query e fare clic su **Esegui**. Questo script consente di impostare la modalità non online per il database `Archive` .  
  
    ```sql  
    CREATE DATABASE Archive ON  
    PRIMARY ( NAME = Arch1,  
        FILENAME = 'c:\moved_location\archdat1.mdf'),  
    FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = Arch3,  
        FILENAME = 'c:\moved_location\filestream1')  
    LOG ON  ( NAME = Archlog1,  
        FILENAME = 'c:\moved_location\archlog1.ldf')  
    FOR ATTACH  
    GO  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
  
