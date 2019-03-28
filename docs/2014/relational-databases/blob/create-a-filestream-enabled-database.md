---
title: Creare un database abilitato per FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FILESTREAM-enabled databases
ms.assetid: 0fc16356-76f7-44b8-a58b-f0b7c43694ec
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 65de151b2ea2bb59330bae0fa94c9e15d67e4a47
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533543"
---
# <a name="create-a-filestream-enabled-database"></a>Creazione di un database abilitato per FILESTREAM
  In questo argomento viene illustrato come creare un database che supporti FILESTREAM. Poiché in FILESTREAM viene utilizzato un tipo speciale di filegroup, quando si crea il database è necessario specificare la clausola CONTAINS FILESTREAM per almeno un filegroup.  
  
 Un filegroup FILESTREAM può contenere più di un file. Per un esempio di codice che illustra come creare un filegroup FILESTREAM contenente più file, vedere [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
### <a name="to-create-a-filestream-enabled-database"></a>Per creare un database abilitato per FILESTREAM  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic su **Nuova query** per visualizzare l'editor di query.  
  
2.  Copia il [!INCLUDE[tsql](../../includes/tsql-md.md)] codice crea un database abilitato per FILESTREAM denominato Archive.  
  
    > [!NOTE]  
    >  Per eseguire questo script, è necessario che la directory C:\Data esista.  
  
3.  Per compilare il database, fare clic su **Esegui**.  
  
## <a name="example"></a>Esempio  
 Nel codice di esempio seguente viene creato un database denominato `Archive`. Il database contiene tre filegroup: `PRIMARY`, `Arch1`e `FileStreamGroup1`. `PRIMARY` e `Arch1` sono filegroup normali che non possono contenere dati FILESTREAM. `FileStreamGroup1` è il filegroup `FILESTREAM` .  
  
```sql  
CREATE DATABASE Archive   
ON  
PRIMARY ( NAME = Arch1,  
    FILENAME = 'c:\data\archdat1.mdf'),  
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = Arch3,  
    FILENAME = 'c:\data\filestream1')  
LOG ON  ( NAME = Archlog1,  
    FILENAME = 'c:\data\archlog1.ldf')  
GO  
```  
  
 Per un filegroup `FILESTREAM` , `FILENAME` fa riferimento a un percorso. È necessario che il percorso fino all'ultima cartella esista già, mentre l'ultima cartella non deve essere presente. In questo esempio è necessario che `c:\data` esista. La sottocartella `filestream1` tuttavia non può esistere quando si esegue l'istruzione `CREATE DATABASE` . Per altre informazioni sulla sintassi, vedere [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
 Dopo avere eseguito l'esempio precedente, nella cartella c:\Data\filestream1 sono presenti il file filestream.hdr e la cartella $FSLOG. Il file filestream.hdr è un file di intestazione per il contenitore FILESTREAM.  
  
> [!IMPORTANT]  
>  Il file filestream.hdr è un importante file di sistema. Tale file contiene informazioni di intestazione di FILESTREAM. Non rimuoverlo o modificarlo.  
  
 Per database esistenti, è possibile utilizzare l'istruzione [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) per aggiungere un filegroup FILESTREAM.  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
