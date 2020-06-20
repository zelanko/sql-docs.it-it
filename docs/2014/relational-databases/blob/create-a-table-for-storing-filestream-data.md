---
title: Creare una tabella per archiviare dati FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], table storage
ms.assetid: 029c3059-5c83-43e2-a859-9027031b7de1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 484d7b58ce949df79dc7e17ee4dc7307b70c0154
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955619"
---
# <a name="create-a-table-for-storing-filestream-data"></a>Creazione di una tabella per archiviare dati FILESTREAM
  In questo argomento viene illustrato come creare una tabella per archiviare dati FILESTREAM.  
  
 Quando il database presenta un filegroup FILESTREAM, è possibile creare o modificare tabelle per archiviare i dati FILESTREAM. Per specificare che una colonna che contiene dati FILESTREAM, creare una colonna `varbinary(max)` e aggiungere l'attributo FILESTREAM.  
  
### <a name="to-create-a-table-to-store-filestream-data"></a>Per creare una tabella per archiviare dati FILESTREAM  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic su **Nuova query** per visualizzare l'editor di query.  
  
2.  Copiare il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] dall'esempio seguente e incollarlo nell'Editor di query. Tramite il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] viene creata una tabella abilitata per FILESTREAM denominata Records.  
  
3.  Per creare la tabella, fare clic su **Esegui**.  
  
## <a name="example"></a>Esempio  
 Nel codice di esempio seguente viene descritto come creare una tabella denominata `Records`. La colonna `Id` è una colonna `ROWGUIDCOL` ed è necessaria per utilizzare dati FILESTREAM con API Win32. La colonna `SerialNumber` è di tipo `UNIQUE INTEGER`. La colonna `Chart` è una colonna `FILESTREAM` e viene utilizzata per archiviare `Chart` nel file system.  
  
> [!NOTE]  
>  Questo esempio fa riferimento al database Archive creato in [Creazione di un database abilitato per FILESTREAM](create-a-filestream-enabled-database.md).  
  
 [!code-sql[FILESTREAM#FS_CreateTable](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_createtable)]  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
