---
title: Crittografia di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], about encryption
- security [SQL Server], encryption
- cryptography [SQL Server], about cryptography
ms.assetid: ead0150e-4943-4ad5-84c8-36f85c7278f4
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3fea2c9fdd532385378e2c66af08eefd4804442
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "74957314"
---
# <a name="sql-server-encryption"></a>Crittografia di SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La crittografia è il processo che consiste nell'offuscare i dati tramite l'utilizzo di una chiave o di una password. È in grado di rendere i dati inutilizzabili se non si dispone della chiave di decrittografia o password corrispondente. La crittografia non risolve i problemi relativi al controllo di accesso, ma migliora la sicurezza limitando la perdita di dati anche se il controllo di accesso viene eluso. Se, ad esempio, il computer host del database è configurato scorrettamente e un pirata informatico ottiene dati riservati, le informazioni sottratte potrebbero essere inutilizzabili se crittografate.  
  

> [!IMPORTANT]  
>  Sebbene la crittografia sia un strumento prezioso per garantire la sicurezza, se ne sconsiglia l'utilizzo per tutti i dati o le connessioni. Per decidere se implementare la crittografia oppure no, considerare le modalità di accesso ai dati utilizzate dagli utenti. Se per accedere gli utenti utilizzano una rete pubblica, la crittografia dei dati potrebbe essere necessaria per aumentare il livello di sicurezza. Tuttavia, se tutti accedono attraverso una configurazione di Intranet sicura, la crittografia potrebbe non essere necessaria. L'utilizzo della crittografia comporta anche l'adozione di una strategia di manutenzione per password, chiavi e certificati.  
  
> [!NOTE]  
>  Le informazioni più recenti sulla sicurezza a livello di trasporto (TLS1.2) sono disponibili nell'articolo [Supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/kb/3135244).  

È possibile utilizzare la crittografia in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per connessioni, dati e stored procedure. Gli argomenti seguenti includono altre informazioni sulla crittografia in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

 [Gerarchia di crittografia](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
 Informazioni sulla gerarchia di crittografia in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Scelta di un algoritmo di crittografia](../../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
 Informazioni sulla selezione di un algoritmo di crittografia efficace.  
  
 [Transparent Data Encryption &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
 Informazioni generali sulla crittografia trasparente dei dati.  
  
 [Chiavi di crittografia del database e di SQL Server &#40;Motore di database&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], le chiavi di crittografia sono costituite da una combinazione di chiavi pubbliche, private e simmetriche utilizzate per proteggere dati riservati. In questa sezione vengono illustrate l'implementazione e la gestione delle chiavi di crittografia.  
  
 [Always Encrypted &#40;Motore di database&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
 Garantisce che gli amministratori del database locale, gli operatori di database cloud o altri utenti con privilegi elevati, ma non autorizzati, non possano accedere ai dati crittografati.  
  
 [Maschera dati dinamica](../../../relational-databases/security/dynamic-data-masking.md)  
 Limita l'esposizione dei dati sensibili nascondendoli agli utenti senza privilegi.  
  
 [Certificati SQL Server e chiavi simmetriche](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)  
 Informazioni sull'uso della crittografia a chiave pubblica.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Sicurezza di SQL Server](../../../relational-databases/security/securing-sql-server.md)  
 Panoramica della sicurezza della piattaforma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e del funzionamento con gli utenti e gli oggetti a protezione diretta.  

[Panoramica delle funzionalità di sicurezza del database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
</br>Panoramica della sicurezza del database SQL di Azure per la protezione dei dati, il controllo dell'accesso e il monitoraggio proattivo.
  
 [Funzioni di crittografia &#40;Transact-SQL&#41;](../../../t-sql/functions/cryptographic-functions-transact-sql.md)  
 Informazioni sull'implementazione delle funzioni di crittografia.  
  
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
 Informazioni sull'utilizzo di una password per la crittografia dei dati.  
  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)  
 Informazioni sull'utilizzo di una chiave simmetrica per la crittografia dei dati.  
  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)  
 Informazioni sull'utilizzo di una chiave simmetrica per la crittografia dei dati.  
  
 [ENCRYPTBYCERT &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbycert-transact-sql.md)  
 Informazioni sull'utilizzo di un certificato per la crittografia dei dati.  
  
## <a name="external-resources"></a>Risorse esterne  
 [Microsoft TechNet: SQL Server TechCenter: Sicurezza e protezione di SQL Server 2012](https://download.microsoft.com/download/8/F/A/8FABACD7-803E-40FC-ADF8-355E7D218F4C/SQL_Server_2012_Security_Best_Practice_Whitepaper_Apr2012.docx)  
 Informazioni aggiornate sulla sicurezza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)   
 [Chiavi di crittografia del database e di SQL Server &#40;Motore di database&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)     
 [Abilitare connessioni crittografate al motore di database](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)    
  
  
