---
title: Eseguire il backup della chiave master di un database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], exporting
ms.assetid: 7ad9a0a0-6e4f-4f7b-8801-8c1b9d49c4d8
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 5435b9056d98a5b2dc0835bfcd0e60865c1686b4
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957265"
---
# <a name="back-up-a-database-master-key"></a>Backup della chiave master di un database
  In questo argomento viene descritto come eseguire il backup di una chiave master del database in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La chiave master viene usata per crittografare altre chiavi e certificati all'interno di un database. Se questa chiave viene eliminata oppure danneggiata, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] potrebbe non essere in grado di decrittografare tali chiavi e i dati crittografati con tali chiavi verranno di fatto persi. Per tale motivo, è consigliabile eseguire il backup della chiave master di un database e archiviare la copia di backup in un altro luogo adeguatamente protetto.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   [Per eseguire il backup di una chiave master del database utilizzando Transact-SQL](#Procedure)  
  
##  <a name="BeforeYouBegin"></a>Prima di iniziare  
  
###  <a name="Restrictions"></a>Limitazioni e restrizioni  
  
-   È necessario aprire e pertanto decrittografare la chiave master prima di eseguirne il backup. Se è crittografata con la chiave master del servizio, non è necessario aprire in modo esplicito la chiave master. Se invece la chiave master è crittografata solo con una password dovrà essere aperta in modo esplicito.  
  
-   È consigliabile creare una copia di backup della chiave master subito dopo la creazione e archiviare il backup in una posizione esterna sicura.  
  
###  <a name="Security"></a>Sicurezza  
  
####  <a name="Permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione CONTROL per il database.  
  
##  <a name="Procedure"></a>Utilizzo di SQL Server Management Studio con Transact-SQL  
  
#### <a name="to-back-up-the-database-master-key"></a>Per eseguire il backup della chiave master di un database  
  
1.  In [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contenente la chiave master del database di cui si desidera eseguire il backup.  
  
2.  Scegliere una password che verrà usata per crittografare la chiave master del database sul supporto di backup. Questa password è soggetta ai controlli di complessità delle password.  
  
3.  Procurarsi un supporto di backup rimovibile per l'archiviazione di una copia della chiave di cui viene eseguito il backup.  
  
4.  Identificare una directory NTFS in cui creare il backup della chiave. Il file specificato nel passaggio successivo verrà creato in questa directory, che è consigliabile proteggere tramite elenchi di controllo di accesso altamente restrittivi.  
  
5.  In **Esplora oggetti**connettersi a un'istanza di [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
6.  Sulla barra Standard fare clic su **Nuova query**.  
  
7.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    -- Creates a backup of the "AdventureWorks2012" master key. Because this master key is not encrypted by the service master key, a password must be specified when it is opened.  
    USE AdventureWorks2012;   
    GO  
    OPEN MASTER KEY DECRYPTION BY PASSWORD = 'sfj5300osdVdgwdfkli7';   
  
    BACKUP MASTER KEY TO FILE = 'c:\temp\exportedmasterkey'   
        ENCRYPTION BY PASSWORD = 'sd092735kjn$&adsg';   
    GO  
    ```  
  
    > [!NOTE]  
    >  Il percorso del file della chiave e della password della chiave (se esistente) sarà diverso da quello indicato in precedenza. Assicurarsi che entrambi siano specifici della configurazione della chiave e del server in uso.  
  
8.  Copiare il file nel supporto di backup e verificare la copia.  
  
9. Archiviare il file in una posizione esterna protetta.  
  
 Per altre informazioni, vedere [OPEN MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/open-master-key-transact-sql) e [BACKUP MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-master-key-transact-sql).  
  
  
