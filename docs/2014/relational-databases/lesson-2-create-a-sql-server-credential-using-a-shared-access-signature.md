---
title: 'Lezione 3: Creazione di una credenziale SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 61a25d1f4e86204d05b3be6bf2a5dbc8cd0474b9
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153828"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>Lezione 3: Creare le credenziali di SQL Server
  In questa lezione verrà creata una credenziale per archiviare le informazioni di sicurezza usate per accedere all'account di archiviazione di Azure.  
  
 Una credenziale di SQL Server è un oggetto utilizzato per archiviare le informazioni di autenticazione necessarie per connettersi a una risorsa all'esterno di SQL Server. Nelle credenziali vengono archiviati il percorso URI del contenitore di archiviazione e i valori della chiave della firma di accesso condivisa. Per ogni contenitore di archiviazione utilizzato da un file di dati o di log, è necessario creare una credenziale di SQL Server il cui nome corrisponda al percorso del contenitore.  
  
 Per informazioni generali sulle credenziali, vedere [credenziali &#40;motore di database&#41;](security/authentication-access/credentials-database-engine.md).  
  
> [!IMPORTANT]  
>  I requisiti per la creazione di una credenziale SQL Server descritta di seguito sono specifici della funzionalità relativa ai [file di dati SQL Server in Azure](databases/sql-server-data-files-in-microsoft-azure.md) . Per informazioni sulla creazione di credenziali per i processi di backup in archiviazione [di Azure, vedere Lezione 2: Creare una credenziale](../tutorials/lesson-2-create-a-sql-server-credential.md)SQL Server.  
  
 Per creare le credenziali di SQL Server, effettuare i passaggi riportati di seguito:  
  
1.  Connettersi a SQL Server Management Studio.  
  
2.  In Esplora oggetti connettersi all'istanza del motore di database installato.  
  
3.  Sulla barra degli strumenti Standard fare clic su Nuova query.  
  
4.  Copiare e incollare l'esempio seguente nella finestra Query e modificare se necessario. L'istruzione seguente consente di creare un SQL Server credenziali per archiviare il certificato di accesso condiviso del contenitore di archiviazione.  
  
    ```sql  
  
    USE master  
    CREATE CREDENTIAL credentialname - this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     Per informazioni dettagliate, vedere [create Credential &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-credential-transact-sql) in documentazione online di SQL Server.  
  
5.  Per visualizzare tutte le credenziali disponibili, è possibile eseguire l'istruzione seguente nella finestra della query:  
  
    ```sql  
    SELECT * from sys.credentials  
    ```  
  
     Per ulteriori informazioni su sys. Credentials, vedere [sys. &#40;Credentials Transact&#41; -SQL](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) in documentazione online di SQL Server.  
  
 **Lezione successiva:**  
  
 [Lezione 4: Creare un database in archiviazione di Azure](lesson-3-database-backup-to-url.md)  
  
  
