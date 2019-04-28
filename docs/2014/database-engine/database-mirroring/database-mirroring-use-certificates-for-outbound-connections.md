---
title: Consenti un Endpoint mirroring del Database per usare i certificati per le connessioni in uscita (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- certificates [SQL Server], database mirroring
- outbound connections [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 464c9096-10d6-4c5e-8bb1-19acba27ad9e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43a55174bae1bb03034ea005749055701884848f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806874"
---
# <a name="allow-a-database-mirroring-endpoint-to-use-certificates-for-outbound-connections-transact-sql"></a>Impostazione dell'endpoint del mirroring del database per l'utilizzo di certificati per le connessioni in uscita (Transact-SQL)
  In questo argomento vengono illustrati i passaggi per la configurazione delle istanze del server per l'utilizzo di certificati per l'autenticazione delle connessioni in uscita per il mirroring del database. Prima di impostare le connessioni in ingresso, è necessario configurare quelle in uscita.  
  
> [!NOTE]  
>  Tutte le connessioni per il mirroring in un'istanza del server utilizzano un singolo endpoint del mirroring del database ed è necessario specificare il metodo di autenticazione dell'istanza del server quando si crea l'endpoint.  
  
 Il processo di configurazione delle connessioni in uscita comprende i passaggi generali seguenti:  
  
1.  Nel database **master** creare una chiave master del database.  
  
2.  Nel database **master** creare un certificato crittografato nell'istanza del server.  
  
3.  Creare un endpoint per l'istanza del server utilizzando il relativo certificato.  
  
4.  Eseguire il backup del certificato in un file e copiarlo nell'altro sistema o negli altri sistemi.  
  
 È necessario eseguire questa procedura per ogni partner e per il server di controllo del mirroring, se disponibile.  
  
 Questa procedura descrive i vari passaggi, Per ogni passaggio la procedura fornisce un esempio di configurazione di un istanza di server in un sistema denominato HOST_A. Nella sezione di esempio corrispondente vengono indicati gli stessi passaggi per un'altra istanza di server in un sistema denominato HOST_B.  
  
## <a name="procedure"></a>Routine  
  
#### <a name="to-configure-server-instances-for-outbound-mirroring-connections-on-hosta"></a>Per configurare le istanze del server per le connessioni per il mirroring in uscita (On HOST_A)  
  
1.  Nel database **master** creare la chiave master del database, se non è già presente. Per visualizzare le chiavi esistenti per un database, usare la vista del catalogo [sys.symmetric_keys](/sql/relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql) .  
  
     Per creare la chiave master del database, utilizzare il comando [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente:  
  
    ```  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<1_Strong_Password!>';  
    GO  
    ```  
  
     Utilizzare una password complessa univoca e archiviarla in una posizione sicura.  
  
     Per altre informazioni, vedere [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql) e [Creazione della chiave master di un database](../../relational-databases/security/encryption/create-a-database-master-key.md).  
  
2.  Nel database **master** creare un certificato crittografato nell'istanza del server da usare per le connessioni in uscita per il mirroring del database.  
  
     Per creare, ad esempio, un certificato per il sistema HOST_A:  
  
    > [!IMPORTANT]  
    >  Se si desidera utilizzare il certificato per più di un anno, specificare la data di scadenza in base all'ora UTC tramite l'opzione EXPIRY_DATE nell'istruzione CREATE CERTIFICATE. È inoltre consigliabile utilizzare SQL Server Management Studio per creare una regola di gestione basata su criteri per ricevere un avviso quando i certificati stanno scadendo. Usando la finestra di dialogo **Crea nuova condizione** di Gestione criteri creare questa regola nel campo **@ExpirationDate** del facet **Certificato** . Per altre informazioni, vedere [Amministrazione di server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md) e [Sicurezza di SQL Server](../../relational-databases/security/securing-sql-server.md).  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_A_cert   
       WITH SUBJECT = 'HOST_A certificate for database mirroring',   
       EXPIRY_DATE = '11/30/2013';  
    GO  
    ```  
  
     Per altre informazioni, vedere [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql).  
  
     Per visualizzare i certificati nel database**master**, usare le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti:  
  
    ```  
    USE master;  
    SELECT * FROM sys.certificates;  
    ```  
  
     Per altre informazioni, vedere [sys.certificates &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-certificates-transact-sql).  
  
3.  Verificare che in ognuna delle istanze del server sia presente l'endpoint del mirroring del database.  
  
     Se per l'istanza del server è già presente un endpoint del mirroring del database, riutilizzare tale endpoint per tutte le altre sessioni avviate nella stessa istanza. Per determinare se in un'istanza del server è presente un endpoint del mirroring del database e per visualizzarne la configurazione, utilizzare l'istruzione seguente:  
  
    ```  
    SELECT name, role_desc, state_desc, connection_auth_desc, encryption_algorithm_desc   
       FROM sys.database_mirroring_endpoints;  
    ```  
  
     Se non sono presenti endpoint, creare un endpoint che utilizzi questo certificato per le connessioni in uscita e che utilizzi le credenziali del certificato per la verifica nell'altro sistema. Si tratta di un endpoint valido per l'intero server, utilizzato da tutte le sessioni di mirroring a cui partecipa l'istanza del server.  
  
     Per creare, ad esempio, un endpoint del mirroring per l'istanza del server di esempio in HOST_A.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
       STATE = STARTED  
       AS TCP (  
          LISTENER_PORT=7024  
          , LISTENER_IP = ALL  
       )   
       FOR DATABASE_MIRRORING (   
          AUTHENTICATION = CERTIFICATE HOST_A_cert  
          , ENCRYPTION = REQUIRED ALGORITHM AES  
          , ROLE = ALL  
       );  
    GO  
    ```  
  
     Per altre informazioni, vedere [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql).  
  
4.  Eseguire il backup del certificarlo e copiarlo nell'altro o negli altri sistemi. Si tratta di un'operazione necessaria per configurare le connessioni in ingresso nell'altro sistema.  
  
    ```  
    BACKUP CERTIFICATE HOST_A_cert TO FILE = 'C:\HOST_A_cert.cer';  
    GO  
    ```  
  
     Per altre informazioni, vedere [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql).  
  
     Copiare questo certificato utilizzando un metodo che ne garantisca la protezione. È estremamente importante garantire la protezione di tutti i certificati.  
  
 Tramite il codice di esempio del passaggio precedente vengono configurate le connessioni in uscita in HOST_A.  
  
 È ora necessario eseguire i rispettivi passaggi in uscita per HOST_B. I passaggi sono illustrati nella sezione di esempio indicata di seguito.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata la configurazione di HOST_B per le connessioni in uscita.  
  
```  
USE master;  
--Create the database Master Key, if needed.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<Strong_Password_#2>';  
GO  
-- Make a certifcate on HOST_B server instance.  
CREATE CERTIFICATE HOST_B_cert   
   WITH SUBJECT = 'HOST_B certificate for database mirroring',   
   EXPIRY_DATE = '11/30/2013';  
GO  
--Create a mirroring endpoint for the server instance on HOST_B.  
CREATE ENDPOINT Endpoint_Mirroring  
   STATE = STARTED  
   AS TCP (  
      LISTENER_PORT=7024  
      , LISTENER_IP = ALL  
   )   
   FOR DATABASE_MIRRORING (   
      AUTHENTICATION = CERTIFICATE HOST_B_cert  
      , ENCRYPTION = REQUIRED ALGORITHM AES  
      , ROLE = ALL  
   );  
GO  
--Backup HOST_B certificate.  
BACKUP CERTIFICATE HOST_B_cert TO FILE = 'C:\HOST_B_cert.cer';  
GO   
--Using any secure copy method, copy C:\HOST_B_cert.cer to HOST_A.  
```  
  
 Copiare il certificato nell'altro sistema utilizzando un metodo che ne garantisca la protezione. È estremamente importante garantire la protezione di tutti i certificati.  
  
> [!IMPORTANT]  
>  Dopo avere configurato le connessioni in uscita, è necessario configurare quelle in ingresso in ogni istanza del server per l'altra o le altre istanze. Per altre informazioni, vedere [Impostazione dell'endpoint del mirroring del database per l'utilizzo di certificati per le connessioni in entrata &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md).  
  
 Per informazioni sulla creazione di un database mirror e un esempio di Transact-SQL, vedere [Preparazione di un database mirror per il mirroring &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
 Per un esempio di Transact-SQL di stabilire una sessione in modalità a prestazioni elevate, vedere [esempio: Configurare tramite certificati di mirroring del Database &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md).  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 A meno che la sicurezza della rete in uso non sia già garantita, è consigliabile utilizzare la crittografia per le connessioni per il mirroring del database.  
  
 Quando si copia un certificato in un altro sistema, utilizzare un metodo di copia sicuro.  
  
## <a name="see-also"></a>Vedere anche  
 [Scelta di un algoritmo di crittografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [Preparazione di un database mirror per il mirroring &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)   
 [Esempio: Configurare tramite certificati di mirroring del Database &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)   
 [Endpoint del mirroring del database &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [Risolvere i problemi relativi alla configurazione del mirroring del database &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)   
 [Impostazione di un database mirror crittografato](set-up-an-encrypted-mirror-database.md)  
  
  
