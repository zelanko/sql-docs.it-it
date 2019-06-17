---
title: Eseguire il backup della chiave master del servizio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server], exporting
ms.assetid: f60b917c-6408-48be-b911-f93b05796904
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 23d4a24811c545bc69b41cb43bfc3f6b957eddf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011536"
---
# <a name="back-up-the-service-master-key"></a>Backup della chiave master del servizio
  In questo argomento viene descritto come eseguire il backup di una chiave master del servizio in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La chiave master del servizio è l'elemento radice della gerarchia di crittografia. È consigliabile crearne una copia di backup e archiviarla in una posizione esterna sicura. La creazione di questa copia di backup dovrebbe essere una delle prime operazioni amministrative eseguite nel server.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   [Per eseguire il backup della chiave master del servizio](#Procedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   È necessario aprire e pertanto decrittografare la chiave master prima di eseguirne il backup. Se crittografata con la chiave master del servizio, non è necessario che la chiave master venga aperta in modo esplicito. Tuttavia, se la chiave master viene crittografata solo con una password, è necessario aprirla in modo esplicito.  
  
-   È consigliabile creare una copia di backup della chiave master subito dopo la creazione e archiviare il backup in una posizione esterna sicura.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione CONTROL per il database.  
  
##  <a name="Procedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-back-up-the-service-master-key"></a>Per eseguire il backup della chiave master del servizio  
  
1.  In [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contenente la chiave master del servizio di cui si desidera eseguire il backup.  
  
2.  Scegliere una password da utilizzare per crittografare la chiave master del servizio nel supporto di backup. Questa password è soggetta ai controlli di complessità delle password. Per ulteriori informazioni, vedere [Password Policy](../password-policy.md).  
  
3.  Procurarsi un supporto di backup rimovibile per l'archiviazione di una copia della chiave di cui viene eseguito il backup.  
  
4.  Identificare una directory NTFS in cui creare il backup della chiave. Il file specificato nel passaggio successivo verrà creato in questa directory, che è consigliabile proteggere tramite elenchi di controllo di accesso altamente restrittivi.  
  
5.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
6.  Sulla barra Standard fare clic su **Nuova query**.  
  
7.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- Creates a backup of the "AdventureWorks2012" master key.  
    -- Because this master key is not encrypted by the service master key, a password must be specified when it is opened.  
    USE AdventureWorks2012;  
    GO  
    BACKUP SERVICE MASTER KEY TO FILE = 'c:\temp_backups\keys\service_master_ key'   
        ENCRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
    GO  
    ```  
  
    > [!NOTE]  
    >  Il percorso del file della chiave e della password della chiave (se esistente) sarà diverso da quello indicato in precedenza. Assicurarsi che entrambi siano specifici della configurazione della chiave e del server in uso.  
  
8.  Copiare il file nel supporto di backup e verificare la copia.  
  
9. Archiviare il file in una posizione esterna protetta.  
  
 Per altre informazioni, vedere [OPEN MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/open-master-key-transact-sql) e [BACKUP MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-master-key-transact-sql).  
  
  
