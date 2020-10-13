---
title: Extensible Key Management (EKM) | Microsoft Docs
description: Informazioni su come configurare e usare Extensible Key Management e sull'integrazione con le funzionalità di crittografia dei dati per SQL Server.
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Key Management
- Extensible Key Management
- EKM, described
ms.assetid: 9bfaf500-2d1e-4c02-b041-b8761a9e695b
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 0524aa4738ae7003d763422c20db17e39e89e964
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867843"
---
# <a name="extensible-key-management-ekm"></a>Extensible Key Management (EKM)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornisce funzionalità di crittografia dei dati insieme a *Extensible Key Management* (EKM), l'uso del provider di *API di crittografia Microsoft* (MSCAPI) per la crittografia e la generazione di chiavi. Le chiavi di crittografia per dati e la crittografia delle chiavi vengono create nei contenitori di chiave temporanei e devono essere esportate da un provider prima di essere archiviate nel database. Questo approccio consente la gestione delle chiavi che include una gerarchia delle chiavi di crittografia e un backup delle chiavi, che devono essere gestiti da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Con la crescente richiesta di conformità con le normative e il problema della privacy dei dati, le organizzazioni sfruttano la crittografia come modalità per fornire una soluzione di "difesa approfondita". Questo approccio risulta spesso poco pratico se si utilizzano solo gli strumenti di gestione della crittografia dei database. I produttori di hardware forniscono prodotti che consentono la gestione aziendale delle chiavi usando i *Moduli di sicurezza hardware* (HSM, Hardware Security Modules). I dispositivi HSM consentono di archiviare le chiavi di crittografia su moduli hardware o software. Questa soluzione è più sicura poiché le chiavi di crittografia non risiedono insieme ai dati di crittografia.  
  
 Alcuni fornitori offrono tali dispositivi sia per la gestione delle chiavi sia per l'accelerazione della crittografia. I dispositivi HSM utilizzano interfacce hardware con un processo server come intermediario tra un'applicazione e un dispositivo HSM. I fornitori implementano anche i provider MSCAPI sui moduli, che possono essere hardware o software. Spesso MSCAPI offre solo un subset delle funzionalità offerte dai dispositivi HSM. I fornitori possono anche offrire software di gestione per dispositivi HSM, configurazione delle chiavi e accesso alle chiavi.  
  
 Le implementazioni HSM variano da fornitore a fornitore e il loro uso con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] richiede un'interfaccia comune. Anche se questa interfaccia è fornita da MSCAPI, supporta solo un subset delle funzionalità HSM. Sono presenti inoltre altre limitazioni, ad esempio l'impossibilità di mantenere a livello nativo le chiavi simmetriche e la mancanza di supporto orientato alla sessione.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Extensible Key Management consente ai fornitori di EKM/HSM di terze parti di registrare i propri moduli in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Quando registrati, gli utenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possono usare le chiavi di crittografia archiviate nei moduli EKM. Ciò consente a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di accedere alle funzionalità di crittografia avanzate supportate da tali moduli, quali la crittografia e decrittografia bulk e le funzioni di gestione delle chiavi quali il periodo di permanenza e la rotazione delle chiavi.  
  
 Quando si esegue [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in una macchina virtuale di Azure, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può usare le chiavi archiviate nell' [insieme di credenziali chiave di Azure](/azure/key-vault/general/basic-concepts). Per altre informazioni, vedere [Extensible Key Management con l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
## <a name="ekm-configuration"></a>Configurazione EKM  
 Extensible Key Management non è disponibile in tutte le edizioni di [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Per impostazione predefinita, Extensible Key Management è disattivato. Per attivare questa caratteristica, utilizzare il comando sp_configure con l'opzione e il valore indicati di seguito, come nell'esempio seguente:  
  
```  
sp_configure 'show advanced', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'EKM provider enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
> [!NOTE]  
>  Se si usa il comando sp_configure per questa opzione su edizioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che non supportano EKM, verrà restituito un errore.  
  
 Per disabilitare la funzionalità, impostare il valore su **0**. Per altre informazioni sull'impostazione delle opzioni del server, vedere [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
## <a name="how-to-use-ekm"></a>Utilizzo di EKM  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Extensible Key Management consente di abilitare le chiavi di crittografia che proteggono i file del database da archiviare in un dispositivo esterno come una smartcard, un dispositivo USB o un modulo EKM/HSM. Consente anche la protezione dei dati da parte degli amministratori del database (tranne i membri del gruppo sysadmin). I dati possono essere crittografati utilizzando le chiavi di crittografia a cui hanno accesso solo gli utenti del database nel modulo esterno EKM/HSM.  
  
 Extensible Key Management fornisce anche i seguenti vantaggi:  
  
-   Controllo delle autorizzazioni aggiuntivo (abilitazione della separazione dei compiti).  
  
-   Prestazioni più elevate per crittografia/decrittografia basata su hardware.  
  
-   Generazione della chiave di crittografia esterna.  
  
-   Archiviazione della chiave di crittografia esterna (separazione fisica di dati e chiavi).  
  
-   Recupero della chiave di crittografia.  
  
-   Memorizzazione della chiave di crittografia esterna (consente di abilitare la rotazione della chiave di crittografia).  
  
-   Recupero della chiave di crittografia più facile.  
  
-   Distribuzione della chiave di crittografia più facile da gestire.  
  
-   Eliminazione sicura della chiave di crittografia.  
  
 È possibile usare Extensible Key Management per una combinazione di nome utente e password o altri metodi definiti dal driver EKM.  
  
> [!CAUTION]  
>  Per la risoluzione di problemi, il supporto tecnico di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] potrebbe richiedere la chiave di crittografia al provider di EKM. Potrebbe anche essere necessario accedere a strumenti o processi del fornitore per risolvere un problema.  
  
### <a name="authentication-with-an-ekm-device"></a>Autenticazione con un dispositivo EKM  
 Un modulo EKM può supportare più di un tipo di autenticazione. Ciascun provider espone solo un tipo di autenticazione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ovvero se il modulo supporta i tipi di autenticazione di base o di altro tipo esporrà l'uno o l'altro, ma non entrambi.  
  
#### <a name="ekm-device-specific-basic-authentication-using-usernamepassword"></a>Autenticazione di base specifica del dispositivo EKM utilizzando nome utente/password  
 Per i moduli EKM che supportano l'autenticazione di base usando una coppia *nome utente/password*, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornisce l'autenticazione trasparente usando le credenziali. Per altre informazioni sulle credenziali, vedere [Credenziali &#40;Motore di database&#41;](../../../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 Una credenziale può essere creata per un provider EKM e sottoposta al mapping a un accesso (sia account Windows che account [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) per accedere a un modulo EKM in base agli accessi. Il campo *identity* della credenziale contiene il nome utente, il campo *secret* contiene una password per la connessione a un modulo EKM.  
  
 Se non è presente una credenziale su cui eseguire il mapping a un accesso per il provider EKM, viene usata la credenziale su cui è stato eseguito il mapping all'account di servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Un accesso può disporre di più credenziali di cui è stato eseguito il mapping all'accesso stesso, se vengono utilizzate per provider EKM distinti. È possibile eseguire il mapping di una sola credenziale per provider EKM per accesso. Sulla stessa credenziale è possibile eseguire il mapping ad altri account di accesso.  
  
#### <a name="other-types-of-ekm-device-specific-authentication"></a>Altri tipi di autenticazione specifica del dispositivo EKM  
 Per i moduli EKM con autenticazione diversa da Windows o combinazioni *nome utente/password* , l'autenticazione deve essere eseguita indipendentemente da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
### <a name="encryption-and-decryption-by-an-ekm-device"></a>Crittografia e decrittografia da un dispositivo EKM  
 È possibile utilizzare le seguenti funzioni e funzionalità per crittografare e decrittografare i dati utilizzando chiavi simmetriche e asimmetriche:  
  
|Funzione o funzionalità|Informazioni di riferimento|  
|-------------------------|---------------|  
|Crittografia con chiave simmetrica|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|Crittografia con chiave asimmetrica|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|EncryptByKey(key_guid, 'cleartext', ...)|[ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)|  
|DecryptByKey(ciphertext, ...)|[DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)|  
|EncryptByAsmKey(key_guid, 'cleartext')|[ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)|  
|DecryptByAsmKey(ciphertext)|[DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
  
#### <a name="database-keys-encryption-by-ekm-keys"></a>Crittografia di chiavi del database tramite chiavi EKM  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può usare le chiavi EKM per crittografare altre chiavi in un database. In un dispositivo EKM è possibile creare e utilizzare sia chiavi simmetriche che asimmetriche. È possibile crittografare chiavi simmetriche native (non EKM) con chiavi asimmetriche EKM.  
  
 Nel seguente esempio viene creata una chiave simmetrica del database e viene crittografata utilizzando una chiave in un modulo EKM.  
  
```  
CREATE SYMMETRIC KEY Key1  
WITH ALGORITHM = AES_256  
ENCRYPTION BY EKM_AKey1;  
GO  
--Open database key  
OPEN SYMMETRIC KEY Key1  
DECRYPTION BY EKM_AKey1  
```  
  
 Per altre informazioni sulle chiavi del server e del database in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Chiavi di crittografia del database e di SQL Server &#40;Motore di database&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md).  
  
> [!NOTE]  
>  Non è possibile crittografare una chiave EKM con un'altra chiave EKM.  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non supporta la firma di moduli con chiavi asimmetriche generate dal provider EKM.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Opzione di configurazione del server EKM provider enabled](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
  
 [Abilitare TDE in SQL Server con EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
 [Extensible Key Management con l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [sys.cryptographic_providers &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)   
 [sys.dm_cryptographic_provider_sessions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-sessions-transact-sql.md)   
 [sys.dm_cryptographic_provider_properties &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-properties-transact-sql.md)   
 [sys.dm_cryptographic_provider_algorithms &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-algorithms-transact-sql.md)   
 [sys.dm_cryptographic_provider_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-keys-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Eliminare e ricreare chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Aggiungere e rimuovere le chiavi di crittografia per una distribuzione con scalabilità orizzontale &#40;Gestione configurazione SSRS&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [Backup della chiave master del servizio](../../../relational-databases/security/encryption/back-up-the-service-master-key.md)   
 [Ripristino della chiave master del servizio](../../../relational-databases/security/encryption/restore-the-service-master-key.md)   
 [Creazione della chiave master di un database](../../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [Backup della chiave master di un database](../../../relational-databases/security/encryption/back-up-a-database-master-key.md)   
 [Ripristino di una chiave master del database](../../../relational-databases/security/encryption/restore-a-database-master-key.md)   
 [Creare chiavi simmetriche identiche su due server](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
