---
title: 'Lezione 3: Creare una credenziale di SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bb40218b2547f14634c060f2c242318101d0ea7b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524917"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>Lezione 3: Creare le credenziali di SQL Server
  In questa lezione verranno create le credenziali per archiviare le informazioni di sicurezza utilizzate per accedere all'account di Archiviazione di Windows Azure.  
  
 Una credenziale di SQL Server è un oggetto utilizzato per archiviare le informazioni di autenticazione necessarie per connettersi a una risorsa all'esterno di SQL Server. Nelle credenziali vengono archiviati il percorso URI del contenitore di archiviazione e i valori della chiave della firma di accesso condivisa. Per ogni contenitore di archiviazione utilizzato da un file di dati o di log, è necessario creare una credenziale di SQL Server il cui nome corrisponda al percorso del contenitore.  
  
 Per informazioni generali sulle credenziali, vedere [credenziali di &#40;motore di Database&#41;](security/authentication-access/credentials-database-engine.md).  
  
> [!IMPORTANT]  
>  I requisiti per la creazione di una credenziale di SQL Server descritta di seguito sono specifici per il [file di dati di SQL Server in Windows Azure](databases/sql-server-data-files-in-microsoft-azure.md) funzionalità. Per informazioni sulla creazione delle credenziali per i processi di backup in archiviazione di Azure, vedere [lezione 2: Creare una credenziale di SQL Server](../tutorials/lesson-2-create-a-sql-server-credential.md).  
  
 Per creare le credenziali di SQL Server, effettuare i passaggi riportati di seguito:  
  
1.  Connettersi a SQL Server Management Studio.  
  
2.  In Esplora oggetti connettersi all'istanza del motore di database installato.  
  
3.  Sulla barra degli strumenti Standard fare clic su Nuova query.  
  
4.  Copiare e incollare l'esempio seguente nella finestra Query e modificare se necessario. L'istruzione seguente crea una credenziale di SQL Server per archiviare il certificato di accesso condiviso del contenitore di archiviazione.  
  
    ```tsql  
  
    USE master  
    CREATE CREDENTIAL credentialname - this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     Per informazioni dettagliate, vedere [CREATE CREDENTIAL &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-credential-transact-sql) nella documentazione Online di SQL Server.  
  
5.  Per visualizzare tutte le credenziali disponibili, è possibile eseguire l'istruzione seguente nella finestra della query:  
  
    ```tsql  
    SELECT * from sys.credentials  
    ```  
  
     Per altre informazioni su Sys. Credentials, vedere [Sys. Credentials &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) nella documentazione Online di SQL Server.  
  
 **Lezione successiva:**  
  
 [Lezione 4: Creare un database in archiviazione di Microsoft Azure](lesson-3-database-backup-to-url.md)  
  
  
