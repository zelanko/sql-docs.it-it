---
title: Centro di sicurezza per il motore di database di SQL Server e il database SQL di Azure | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- SQL Server, security
- security [SQL Server]
- database security [SQL Server]
- databases [SQL Server], security
ms.assetid: dfb39d16-722a-4734-94bb-98e61e014ee7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 1fffca14e9c30c5fd01cff88b7bb90608eb9d30d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185389"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>Centro di sicurezza per il motore di database di SQL Server e il database SQL di Azure
  Questa pagina fornisce i collegamenti che consentono di individuare le informazioni necessarie su sicurezza e protezione nel [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e nel [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].  
  
> [!NOTE]  
>  Alle funzionalità di [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] vengono apportati sempre nuovi miglioramenti. Vedere la versione più recente di questo argomento per le ultime novità sul [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
|Autenticazione: Chi sei?|Autorizzazione: Cosa potete fare?|Crittografia: Archiviazione dei dati segreti|Sicurezza della connessione: Limitazioni e sicurezza|Controllo: Registrazione dell'accesso|  
|----------------------------------|-------------------------------------|-------------------------------------|---------------------------------------------------|--------------------------------|  
|**Scelta del tipo di autenticazione**<br /><br /> [![Mappa del Centro sicurezza: autenticazione Windows](../../database-engine/media/security-center-map-windows-authenticaion.png "mappa del Centro sicurezza: autenticazione Windows")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> <br /><br /> [![Mappa del Centro sicurezza SQL Server autenticazione](../../database-engine/media/security-center-map-sql-authenticaion.png "mappa del Centro sicurezza SQL autenticazione Server")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> **Dove viene eseguita l'autenticazione**<br /><br /> [![Il Centro sicurezza mapping account di accesso e utenti](../../database-engine/media/security-center-map-logins-users.png "Centro sicurezza mapping account di accesso e utenti")](https://msdn.microsoft.com/library/aa337562.aspx)<br /><br /> <br /><br /> [![Mappa del Centro sicurezza: utenti di Database indipendente](../../database-engine/media/security-center-map-contained-users.png "mappa del Centro sicurezza: utenti di Database indipendente")](https://msdn.microsoft.com/library/ff929188.aspx)<br /><br /> **Uso di altre identità**<br /><br /> [![Il Centro sicurezza mappa credenziali](../../database-engine/media/security-center-map-credentials.png "credenziali mappa il Centro sicurezza")](https://msdn.microsoft.com/library/ms161950.aspx)<br /><br /> [![Mappa del Centro sicurezza: Execute As Login](../../database-engine/media/security-center-map-exec-as-login.png "mappa del Centro sicurezza: Execute As Login")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> [![Mappa del Centro sicurezza: Execute As User](../../database-engine/media/security-center-map-exec-as-user.png "mappa del Centro sicurezza: Execute As User")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")|**Concessione, revoca e negazione delle autorizzazioni**<br /><br /> [![Centro sicurezza di eseguire il mapping di classi a protezione diretta](../../database-engine/media/security-center-map-securable-classes.png "Centro sicurezza di eseguire il mapping di classi a protezione diretta")](https://msdn.microsoft.com/library/ms190401.aspx)<br /><br /> [![Mappa del Centro sicurezza: autorizzazioni Server](../../database-engine/media/security-center-map-srv-perms.png "mappa del Centro sicurezza: autorizzazioni Server")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> [![Mappa del Centro sicurezza: autorizzazioni Database](../../database-engine/media/security-center-map-db-perms.png "mappa del Centro sicurezza: autorizzazioni Database")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> **Sicurezza in base ai ruoli**<br /><br /> [![Ruoli Server mappa del Centro sicurezza](../../database-engine/media/security-center-map-srv-roles.png "ruoli Server mappa del Centro sicurezza")](https://msdn.microsoft.com/library/ms188659.aspx)<br /><br /> [![Ruoli Database della mappa del Centro sicurezza](../../database-engine/media/security-center-map-db-roles.png "ruoli Database della mappa del Centro sicurezza")](https://msdn.microsoft.com/library/ms189121.aspx)<br /><br /> `Restricting Data Access to Selected Data Elements`<br /><br /> [![Procedure e viste mappa il Centro sicurezza PC](../../database-engine/media/security-center-map-view-procs.png "procedure e le visualizzazioni mappa di Centro sicurezza")](https://msdn.microsoft.com/library/ms175503.aspx)<br /><br /> [![Sicurezza a livello di riga mappa il Centro sicurezza PC](../../database-engine/media/security-center-map-row-level-sec.png "sicurezza a livello di riga mappa il Centro sicurezza")](https://msdn.microsoft.com/library/dn765131.aspx)<br /><br /> [![Maschera dati dinamica della mappa del Centro sicurezza](../../database-engine/media/security-center-map-data-masking.png "maschera dati dinamica della mappa del Centro sicurezza")](http://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [![Mappa del Centro sicurezza: oggetti firmati](../../database-engine/media/security-center-map-signed-objects.png "mappa del Centro sicurezza: oggetti firmati")](https://msdn.microsoft.com/library/ms181700.aspx)<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")|**Crittografia dei file**<br /><br /> [![Il Centro sicurezza mappa BitLocker](../../database-engine/media/security-center-map-bitlocker.png "BitLocker mappa il Centro sicurezza")](https://support.microsoft.com/en-us/kb/2855131)<br /><br /> [![Mappa del Centro sicurezza: crittografia NTFS](../../database-engine/media/security-center-map-ntfs-encryp.png "mappa del Centro sicurezza: crittografia NTFS")](https://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [![Security Center Map TDE](../../database-engine/media/security-center-map-tde.png "Security Center Map TDE")](https://msdn.microsoft.com/library/bb934049.aspx)<br /><br /> [![Mappa del Centro sicurezza: crittografia Backup](../../database-engine/media/security-center-map-backup-encryp.png "mappa del Centro sicurezza: crittografia Backup")](https://msdn.microsoft.com/library/dn449489.aspx)<br /><br /> **Crittografia delle origini**<br /><br /> [![Security Center Map EKM](../../database-engine/media/security-center-map-ekm.png "Security Center Map EKM")](https://msdn.microsoft.com/library/bb895340.aspx)<br /><br /> [![Eseguire il mapping di Centro sicurezza di Azure Key Vault](../../database-engine/media/security-center-map-key-vault.png "eseguire il mapping di Centro sicurezza di Azure Key Vault")](http://azure.microsoft.com/documentation/articles/key-vault-get-started/)<br /><br /> **Colonne, dati e chiave di crittografia**<br /><br /> [![Mappa del Centro sicurezza: crittografia mediante certificato](../../database-engine/media/security-center-map-cert.png "mappa del Centro sicurezza: crittografia mediante certificato")](https://msdn.microsoft.com/library/ms188061.aspx)<br /><br /> [![Mappa del Centro sicurezza: crittografia mediante chiave simmetrica](../../database-engine/media/security-center-map-sym-key.png "mappa del Centro sicurezza: crittografia mediante chiave simmetrica")](https://msdn.microsoft.com/library/ms174361.aspx)<br /><br /> [![Mappa del Centro sicurezza: crittografia mediante chiave asimmetrica](../../database-engine/media/security-center-map-asym-key.png "mappa del Centro sicurezza: crittografia mediante chiave asimmetrica")](https://msdn.microsoft.com/library/ms186950.aspx)<br /><br /> [![Mappa del Centro sicurezza: crittografia mediante Passphrase](../../database-engine/media/security-center-map-passphrase.png "mappa del Centro sicurezza: crittografia mediante Passphrase")](https://msdn.microsoft.com/library/ms190357.aspx)|**Protezione con firewall**<br /><br /> [![Mappa del Centro sicurezza PC Windows Firewall del](../../database-engine/media/security-center-map-windows-firewall.png "mappa del Centro sicurezza PC Windows Firewall del")](https://msdn.microsoft.com/library/ms175043.aspx)<br /><br /> [![Mappa il Centro sicurezza: firewall del servizio](../../database-engine/media/security-center-map-service-firewall.png "Firewall del Centro sicurezza mappa servizio")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> [![Firewall del Database della mappa il Centro sicurezza PC](../../database-engine/media/security-center-map-db-firewall.png "Firewall di Database della mappa di Centro sicurezza")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> **Crittografia dei dati in transito**<br /><br /> [![Mappa del Centro sicurezza: SSL forzato](../../database-engine/media/security-center-map-forced-ssl.png "mappa del Centro sicurezza: SSL forzato")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> [![Centro sicurezza di eseguire il mapping SSL facoltative](../../database-engine/media/security-center-map-opt-ssl.png "Centro sicurezza di eseguire il mapping SSL facoltative")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")|**Controllo automatizzato**<br /><br /> [![Il Centro sicurezza mappa SQL Server Audit](../../database-engine/media/security-center-map-sql-audit.png "Centro sicurezza mappa SQL Server Audit")](https://msdn.microsoft.com/library/cc280386.aspx)<br /><br /> [![Il Centro sicurezza mappa SQL Database Audit](../../database-engine/media/security-center-map-sqldb-audit.png "controllo del Database SQL mappa il Centro sicurezza")](http://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> **Controllo personalizzato**<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> [![Il Centro sicurezza mappa trigger](../../database-engine/media/security-center-map-triggers.png "trigger mappa il Centro sicurezza")](https://msdn.microsoft.com/library/ms175941.aspx)<br /><br /> **Conformità**<br /><br /> [![SecCtrCompliance](../../database-engine/media/secctrcompliance.png "SecCtrCompliance")](http://azure.microsoft.com/support/trust-center/services/)<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "segnaposto")<br /><br /> ![Centro sicurezza: legenda](../../database-engine/media/security-center-map-legend.png "Centro sicurezza: legenda")|  
  
## <a name="links-to-specific-related-topics"></a>Collegamenti ad argomenti correlati specifici  
 ![Icona cartella File piccola](../../integration-services/media/filefolder-small.gif "icona cartella File piccola") **autenticazione: Chi sei?**  
 **Chi esegue l'autenticazione? (Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
  
-   [Scegliere una modalità di autenticazione](choose-an-authentication-mode.md)  
  
 **Autenticazione a livello di database master** (account di accesso e utenti di database)  
  
-   [Creazione di un account di accesso di SQL Server](authentication-access/create-a-login.md)  
  
-   [Gestione di database e account di accesso in Database SQL di Azure](https://msdn.microsoft.com/library/ee336235.aspx)  
  
-   [Creazione di un utente di database](authentication-access/create-a-database-user.md)  
  
 **Esegue l'autenticazione a un database utente**  
  
-   [Utenti di database indipendente: rendere portabile un database](contained-database-users-making-your-database-portable.md)  
  
 **Uso di altre identità**  
  
-   [Credenziali &#40;motore di database&#41;](authentication-access/credentials-database-engine.md)  
  
-   [Esecuzione con un altro account di accesso](/sql/t-sql/statements/execute-as-transact-sql)  
  
-   [Esecuzione con un altro utente di database](/sql/t-sql/statements/execute-as-transact-sql)  
  
 ![Icona cartella File piccola](../../integration-services/media/filefolder-small.gif "icona cartella File piccola") **crittografia: Archiviazione dei dati segreti**  
 **Crittografia dei file**  
  
-   [BitLocker (a livello di unità)](https://support.microsoft.com/kb/2855131)  
  
-   [Crittografia NTFS (a livello di cartella)](https://msdn.microsoft.com/library/dd163562.aspx)  
  
-   [Transparent Data Encryption (a livello di file)](encryption/transparent-data-encryption.md)  
  
-   [Crittografia dei backup (a livello di file)](../backup-restore/backup-encryption.md)  
  
 **Crittografia delle origini**  
  
-   [Modulo Extensible Key Management](encryption/extensible-key-management-ekm.md)  
  
-   [Chiavi archiviate nell'insieme di credenziali di Azure](encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 **Colonna, dati e chiave di crittografia**  
  
-   [Crittografia mediante certificato](/sql/t-sql/functions/encryptbycert-transact-sql)  
  
-   [Crittografia mediante chiave asimmetrica](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
  
-   [Crittografia mediante chiave simmetrica](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [Crittografia mediante passphrase](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
  
 ![Icona cartella File piccola](../../integration-services/media/filefolder-small.gif "icona cartella File piccola") **autorizzazione: Cosa potete fare?**  
 **Concessione, revoca e negazione delle autorizzazioni**  
  
-   [Gerarchia delle autorizzazioni &#40;motore di database&#41;](permissions-hierarchy-database-engine.md)  
  
-   [Autorizzazioni](permissions-database-engine.md)  
  
-   [Entità a protezione diretta](securables.md)  
  
 **Sicurezza in base ai ruoli**  
  
-   [Ruoli a livello di server](authentication-access/server-level-roles.md)  
  
-   [Ruoli a livello di database](authentication-access/database-level-roles.md)  
  
 `Restricting Data Access to Selected Data Elements`  
  
-   Uso di [viste](../views/views.md) e [routine](../stored-procedures/stored-procedures-database-engine.md)per limitare l'accesso ai dati  
  
-   [Sicurezza a livello di riga](https://msdn.microsoft.com/library/azure/dn765131.aspx)  
  
-   [Mascheramento dati dinamici](http://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)  
  
-   [Oggetti firmati](/sql/t-sql/statements/add-signature-transact-sql)  
  
 ![Icona cartella File piccola](../../integration-services/media/filefolder-small.gif "icona cartella File piccola") **sicurezza della connessione: Limitazioni e sicurezza**  
 **Protezione con firewall**  
  
-   [Configurazione di Windows Firewall per l'accesso al Motore di database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Impostazioni del firewall del database SQL di Azure](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
-   [Impostazioni del firewall dei servizi di Azure](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
 **Crittografia dei dati in transito**  
  
-   [Secure Sockets Layer per il motore di database](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
-   [Secure Sockets Layer per il database SQL](https://msdn.microsoft.com/library/azure/ff394108.aspx)  
  
 ![Icona cartella File piccola](../../integration-services/media/filefolder-small.gif "icona cartella File piccola") **il controllo: Registrazione dell'accesso**  
 **Controllo automatizzato**  
  
-   [SQL Server Audit &#40;Database Engine&#41;](auditing/sql-server-audit-database-engine.md)  
  
-   [Controllo del database SQL](http://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)  
  
 **Implementazione di controlli personalizzati**  
  
-   Creazione di [DDL Triggers](../triggers/ddl-triggers.md) e di [DML Triggers](../triggers/dml-triggers.md)  
  
 ![Icona cartella File piccola](../../integration-services/media/filefolder-small.gif "icona cartella File piccola") **conformità**  
 **SQL Server**  
  
-   [Criteri comuni](https://go.microsoft.com/fwlink/?LinkId=616319)  
  
 **Database SQL**  
  
-   [Centro protezione Microsoft Azure: Conformità per funzionalità](http://azure.microsoft.com/support/trust-center/services/)  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza di SQL Server](securing-sql-server.md)   
 [Entità &#40;motore di database&#41;](authentication-access/principals-database-engine.md)   
 [Certificati SQL Server e chiavi simmetriche](sql-server-certificates-and-asymmetric-keys.md)   
 [Crittografia di SQL Server](encryption/sql-server-encryption.md)   
 [Configurazione superficie di attacco](surface-area-configuration.md)   
 [Password complesse](strong-passwords.md)   
 [Proprietà di database TRUSTWORTHY](trustworthy-database-property.md)   
 [Caratteristiche e attività del motore di database](../../database-engine/database-engine-features-and-tasks.md)  
  
  
