---
title: Replicare dati in colonne crittografate (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], replicating data
- encryption [SQL Server replication]
- publishing [SQL Server replication], encrypted columns
ms.assetid: d1f8f586-e5a3-4a71-9391-11198d42bfa3
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: cbaf7db0d5c0e4588f22d0048c96e1f7c88d87b0
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907433"
---
# <a name="replicate-data-in-encrypted-columns-sql-server-management-studio"></a>Replicare dati in colonne crittografate (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  La replica consente di pubblicare dati di colonna crittografati. Per decrittografare e utilizzare tali dati nel Sottoscrittore, la chiave utilizzata per crittografare i dati nel server di pubblicazione deve essere presente anche nel Sottoscrittore. La replica non rappresenta un meccanismo protetto per il trasporto di chiavi di crittografia. La chiave di crittografia deve essere ricreata manualmente nel Sottoscrittore. In questo argomento verrà illustrato come crittografare una colonna nel server di pubblicazione e garantire che la chiave di crittografia sia disponibile nel Sottoscrittore.  
  
 I passaggi principali sono i seguenti:  
  
1.  Creare la chiave simmetrica nel server di pubblicazione.  
  
2.  Crittografare i dati della colonna con la chiave simmetrica.  
  
3.  Pubblicare la tabella con la colonna crittografata.  
  
4.  Sottoscrivere la pubblicazione.  
  
5.  Inizializzare la sottoscrizione.  
  
6.  Ricreare la chiave simmetrica nel Sottoscrittore utilizzando i valori del passaggio 1 per ALGORITHM, KEY_SOURCE e IDENTITY_VALUE.  
  
7.  Accedere ai dati della colonna crittografata.  

> [!NOTE]  
>  Per crittografare i dati della colonna è consigliabile utilizzare una chiave simmetrica. La chiave simmetrica può essere protetta in modi diversi nel server di pubblicazione e nel Sottoscrittore.  
  
### <a name="to-create-and-replicate-encrypted-column-data"></a>Per creare e replicare dati di colonne crittografate  
  
1.  Nel server di pubblicazione eseguire [CREATE SYMMETRIC KEY](../../../t-sql/statements/create-symmetric-key-transact-sql.md).  
  
    > [!IMPORTANT]  
    >  Il valore di KEY_SOURCE è rappresentato da dati importanti, utilizzabili per ricreare la chiave simmetrica e decrittografare i dati. KEY_SOURCE deve pertanto essere sempre archiviato e trasportato in modo protetto.  
  
2.  Eseguire [OPEN SYMMETRIC KEY](../../../t-sql/statements/open-symmetric-key-transact-sql.md) per aprire la nuova chiave.  
  
3.  Utilizzare la funzione [EncryptByKey](../../../t-sql/functions/encryptbykey-transact-sql.md) per crittografare i dati della colonna nel server di pubblicazione.  
  
4.  Eseguire [CLOSE SYMMETRIC KEY](../../../t-sql/statements/close-symmetric-key-transact-sql.md) per chiudere la chiave.  
  
5.  Pubblicare la tabella contenente la colonna crittografata. Per altre informazioni, vedere [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
6.  Sottoscrivere la pubblicazione. Per altre informazioni, vedere [Creare una sottoscrizione pull](../../../relational-databases/replication/create-a-pull-subscription.md) o [Creare una sottoscrizione push](../../../relational-databases/replication/create-a-push-subscription.md).  
  
7.  Inizializzare la sottoscrizione. Per altre informazioni, vedere [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
8.  Nel Sottoscrittore eseguire [CREATE SYMMETRIC KEY](../../../t-sql/statements/create-symmetric-key-transact-sql.md) utilizzando i valori del passaggio 1 per ALGORITHM, KEY_SOURCE e IDENTITY_VALUE. È possibile specificare un valore diverso per ENCRYPTION BY.  
  
    > [!IMPORTANT]  
    >  Il valore di KEY_SOURCE è rappresentato da dati importanti, utilizzabili per ricreare la chiave simmetrica e decrittografare i dati. KEY_SOURCE deve pertanto essere sempre archiviato e trasportato in modo protetto.  
  
9. Eseguire [OPEN SYMMETRIC KEY](../../../t-sql/statements/open-symmetric-key-transact-sql.md) per aprire la nuova chiave.  
  
10. Utilizzare la funzione [DecryptByKey](../../../t-sql/functions/decryptbykey-transact-sql.md) per decrittografare i dati replicati nel Sottoscrittore.  
  
11. Eseguire [CLOSE SYMMETRIC KEY](../../../t-sql/statements/close-symmetric-key-transact-sql.md) per chiudere la chiave.  
  
## <a name="example"></a>Esempio  
 In questo esempio verranno creati una chiave simmetrica, un certificato utilizzato per proteggere la chiave simmetrica e una chiave master. Le chiavi verranno create nel database di pubblicazione e verranno utilizzate per creare una colonna crittografata (EncryptedCreditCardApprovalCode) nella tabella `SalesOrderHeader` . Questa colonna verrà pubblicata nella pubblicazione AdvWorksSalesOrdersMerge al posto della colonna non crittografata CreditCardApprovalCode. Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
 [!code-sql[HowTo#sp_PublishEncryptedColumn](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_1.sql)]  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_2.sql)]  
  
## <a name="example"></a>Esempio  
 In questo esempio verrà ricreata la stessa chiave simmetrica nel database di sottoscrizione utilizzando i valori di ALGORITHM, KEY_SOURCE e IDENTITY_VALUE del primo esempio. Si presume che sia già stata inizializzata una sottoscrizione alla pubblicazione AdvWorksSalesOrdersMerge per la replica della colonna crittografata. Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file durante l'archiviazione e il trasporto per evitare accessi non autorizzati.  
  
 [!code-sql[HowTo#sp_SubscriberEncryptedColumn](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_3.sql)]  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Creare chiavi simmetriche identiche su due server](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
