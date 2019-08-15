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
ms.openlocfilehash: 131fb3639f84c1b59796d59bcfff17159da8f063
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028663"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>Centro di sicurezza per il motore di database di SQL Server e il database SQL di Azure
  Questa pagina fornisce i collegamenti che consentono di individuare le informazioni necessarie su sicurezza e protezione nel [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e nel [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].  
  
> [!NOTE]  
>  Alle funzionalità di [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] vengono apportati sempre nuovi miglioramenti. Vedere la versione più recente di questo argomento per le ultime novità sul [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
|Autenticazione informazioni sull'utente|Autorizzazione operazioni consentite|Crittografia archiviazione di dati segreti|Sicurezza della connessione: limitazioni e protezione|Controllo: registrazione dell'accesso|  
|----------------------------------|-------------------------------------|-------------------------------------|---------------------------------------------------|--------------------------------|  
|**Scelta del tipo di autenticazione**<br /><br /> [![Mappa del Centro sicurezza-autenticazione di Windows](../../database-engine/media/security-center-map-windows-authenticaion.png "Mappa del Centro sicurezza-autenticazione di Windows")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> <br /><br /> [![Mappa del Centro sicurezza SQL Server autenticazione](../../database-engine/media/security-center-map-sql-authenticaion.png "Mappa del Centro sicurezza SQL Server autenticazione")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> **Dove viene eseguita l'autenticazione**<br /><br /> [![Mappa del Centro sicurezza-account di accesso e utenti](../../database-engine/media/security-center-map-logins-users.png "Mappa del Centro sicurezza-account di accesso e utenti")](https://msdn.microsoft.com/library/aa337562.aspx)<br /><br /> <br /><br /> [![Mappa del Centro sicurezza. utenti del database indipendente](../../database-engine/media/security-center-map-contained-users.png "Mappa del Centro sicurezza. utenti del database indipendente")](https://msdn.microsoft.com/library/ff929188.aspx)<br /><br /> **Uso di altre identità**<br /><br /> [![Mappa del Centro sicurezza-credenziali](../../database-engine/media/security-center-map-credentials.png "Mappa del Centro sicurezza-credenziali")](https://msdn.microsoft.com/library/ms161950.aspx)<br /><br /> [![Mappa del Centro sicurezza-Esegui come account di accesso](../../database-engine/media/security-center-map-exec-as-login.png "Mappa del Centro sicurezza-Esegui come account di accesso")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> [![Mappa del Centro sicurezza-Esegui come utente](../../database-engine/media/security-center-map-exec-as-user.png "Mappa del Centro sicurezza-Esegui come utente")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")|**Concessione, revoca e negazione delle autorizzazioni**<br /><br /> [![Mappa del Centro sicurezza-classi a protezione diretta](../../database-engine/media/security-center-map-securable-classes.png "Mappa del Centro sicurezza-classi a protezione diretta")](https://msdn.microsoft.com/library/ms190401.aspx)<br /><br /> [![Mappa del Centro sicurezza-autorizzazioni del server](../../database-engine/media/security-center-map-srv-perms.png "Mappa del Centro sicurezza-autorizzazioni del server")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> [![Mappa del Centro sicurezza-autorizzazioni database](../../database-engine/media/security-center-map-db-perms.png "Mappa del Centro sicurezza-autorizzazioni database")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> **Sicurezza in base ai ruoli**<br /><br /> [![Mappa del Centro sicurezza-ruoli del server](../../database-engine/media/security-center-map-srv-roles.png "Mappa del Centro sicurezza-ruoli del server")](https://msdn.microsoft.com/library/ms188659.aspx)<br /><br /> [![Mappa del Centro sicurezza-ruoli del database](../../database-engine/media/security-center-map-db-roles.png "Mappa del Centro sicurezza-ruoli del database")](https://msdn.microsoft.com/library/ms189121.aspx)<br /><br /> `Restricting Data Access to Selected Data Elements`<br /><br /> [![Mappa del Centro sicurezza-viste e procedure](../../database-engine/media/security-center-map-view-procs.png "Mappa del Centro sicurezza-viste e procedure")](https://msdn.microsoft.com/library/ms175503.aspx)<br /><br /> [![Mappa del Centro sicurezza sicurezza a livello di riga](../../database-engine/media/security-center-map-row-level-sec.png "Mappa del Centro sicurezza sicurezza a livello di riga")](https://msdn.microsoft.com/library/dn765131.aspx)<br /><br /> [![Mappa del Centro sicurezza Dynamic Data Masking](../../database-engine/media/security-center-map-data-masking.png "Mappa del Centro sicurezza Dynamic Data Masking")](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [![Mappa del Centro sicurezza-oggetti firmati](../../database-engine/media/security-center-map-signed-objects.png "Mappa del Centro sicurezza-oggetti firmati")](https://msdn.microsoft.com/library/ms181700.aspx)<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")|**Crittografia dei file**<br /><br /> [![Mappa del Centro sicurezza-BitLocker](../../database-engine/media/security-center-map-bitlocker.png "Mappa del Centro sicurezza-BitLocker")](https://support.microsoft.com/en-us/kb/2855131)<br /><br /> [![Mappa del Centro sicurezza-crittografia NTFS](../../database-engine/media/security-center-map-ntfs-encryp.png "Mappa del Centro sicurezza-crittografia NTFS")](https://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [![Mappa del Centro sicurezza](../../database-engine/media/security-center-map-tde.png "Mappa del Centro sicurezza")](https://msdn.microsoft.com/library/bb934049.aspx)<br /><br /> [![Mappa del Centro sicurezza-crittografia del backup](../../database-engine/media/security-center-map-backup-encryp.png "Mappa del Centro sicurezza-crittografia del backup")](https://msdn.microsoft.com/library/dn449489.aspx)<br /><br /> **Crittografia delle origini**<br /><br /> [![Mappa del Centro sicurezza-EKM](../../database-engine/media/security-center-map-ekm.png "Mappa del Centro sicurezza-EKM")](https://msdn.microsoft.com/library/bb895340.aspx)<br /><br /> [![Mappa del Centro sicurezza Azure Key Vault](../../database-engine/media/security-center-map-key-vault.png "Mappa del Centro sicurezza Azure Key Vault")](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)<br /><br /> **Crittografia della chiave di & dati della colonna**<br /><br /> [![Mappa del Centro sicurezza-crittografia mediante certificato](../../database-engine/media/security-center-map-cert.png "Mappa del Centro sicurezza-crittografia mediante certificato")](https://msdn.microsoft.com/library/ms188061.aspx)<br /><br /> [![Mappa del Centro sicurezza-crittografia mediante chiave simmetrica](../../database-engine/media/security-center-map-sym-key.png "Mappa del Centro sicurezza-crittografia mediante chiave simmetrica")](https://msdn.microsoft.com/library/ms174361.aspx)<br /><br /> [![Mappa del Centro sicurezza-crittografia mediante chiave asimmetrica](../../database-engine/media/security-center-map-asym-key.png "Mappa del Centro sicurezza-crittografia mediante chiave asimmetrica")](https://msdn.microsoft.com/library/ms186950.aspx)<br /><br /> [![Mappa del Centro sicurezza-crittografa per passphrase](../../database-engine/media/security-center-map-passphrase.png "Mappa del Centro sicurezza-crittografa per passphrase")](https://msdn.microsoft.com/library/ms190357.aspx)|**Protezione con firewall**<br /><br /> [![Mappa del Centro sicurezza Windows Firewall](../../database-engine/media/security-center-map-windows-firewall.png "Mappa del Centro sicurezza Windows Firewall")](https://msdn.microsoft.com/library/ms175043.aspx)<br /><br /> [![Mappa del Centro sicurezza-firewall del servizio](../../database-engine/media/security-center-map-service-firewall.png "Mappa del Centro sicurezza-firewall del servizio")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> [![Mappa del Centro sicurezza-firewall database](../../database-engine/media/security-center-map-db-firewall.png "Mappa del Centro sicurezza-firewall database")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> **Crittografia dei dati in transito**<br /><br /> [![Mappa del Centro sicurezza-SSL forzato](../../database-engine/media/security-center-map-forced-ssl.png "Mappa del Centro sicurezza-SSL forzato")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> [![Mappa del Centro sicurezza-SSL facoltativo](../../database-engine/media/security-center-map-opt-ssl.png "Mappa del Centro sicurezza-SSL facoltativo")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")|**Controllo automatizzato**<br /><br /> [![Mappa del Centro sicurezza SQL Server controllo](../../database-engine/media/security-center-map-sql-audit.png "Mappa del Centro sicurezza SQL Server controllo")](https://msdn.microsoft.com/library/cc280386.aspx)<br /><br /> [![Mappa del Centro sicurezza-controllo database SQL](../../database-engine/media/security-center-map-sqldb-audit.png "Mappa del Centro sicurezza-controllo database SQL")](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> **Controllo personalizzato**<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> [![Mappa del Centro sicurezza-trigger](../../database-engine/media/security-center-map-triggers.png "Mappa del Centro sicurezza-trigger")](https://msdn.microsoft.com/library/ms175941.aspx)<br /><br /> **Conformità**<br /><br /> [![SecCtrCompliance](../../database-engine/media/secctrcompliance.png "SecCtrCompliance")](https://azure.microsoft.com/support/trust-center/services/)<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Segnaposto](../../database-engine/media/security-center-map-blankplaceholder.png "Segnaposto")<br /><br /> ![Legenda del Centro sicurezza](../../database-engine/media/security-center-map-legend.png "Legenda del Centro sicurezza")|  
  
## <a name="links-to-specific-related-topics"></a>Collegamenti ad argomenti correlati specifici  
 ![Icona della cartella file piccola](../../integration-services/media/filefolder-small.gif "Icona della cartella file piccola") **Autenticazione: Chi sei?**  
 **Chi esegue l'autenticazione? (Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
  
-   [Scegliere una modalità di autenticazione](choose-an-authentication-mode.md)  
  
 **Autenticazione a livello di database master** (account di accesso e utenti di database)  
  
-   [Creazione di un account di accesso di SQL Server](authentication-access/create-a-login.md)  
  
-   [Gestione di database e account di accesso in Database SQL di Azure](https://msdn.microsoft.com/library/ee336235.aspx)  
  
-   [Creazione di un utente di database](authentication-access/create-a-database-user.md)  
  
 **Eseguire l'autenticazione in un database utente**  
  
-   [Utenti di database indipendente: rendere portabile un database](contained-database-users-making-your-database-portable.md)  
  
 **Uso di altre identità**  
  
-   [Credenziali &#40;motore di database&#41;](authentication-access/credentials-database-engine.md)  
  
-   [Esecuzione con un altro account di accesso](/sql/t-sql/statements/execute-as-transact-sql)  
  
-   [Esecuzione con un altro utente di database](/sql/t-sql/statements/execute-as-transact-sql)  
  
 ![Icona della cartella file piccola](../../integration-services/media/filefolder-small.gif "Icona della cartella file piccola") **Crittografia: Archiviazione dei dati segreti**  
 **Crittografia dei file**  
  
-   [BitLocker (a livello di unità)](https://support.microsoft.com/kb/2855131)  
  
-   [Crittografia NTFS (a livello di cartella)](https://msdn.microsoft.com/library/dd163562.aspx)  
  
-   [Transparent Data Encryption (a livello di file)](encryption/transparent-data-encryption.md)  
  
-   [Crittografia dei backup (a livello di file)](../backup-restore/backup-encryption.md)  
  
 **Crittografia delle origini**  
  
-   [Modulo Extensible Key Management](encryption/extensible-key-management-ekm.md)  
  
-   [Chiavi archiviate nell'insieme di credenziali di Azure](encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 **Crittografia di colonne, dati e chiavi**  
  
-   [Crittografia mediante certificato](/sql/t-sql/functions/encryptbycert-transact-sql)  
  
-   [Crittografia mediante chiave asimmetrica](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
  
-   [Crittografia mediante chiave simmetrica](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [Crittografia mediante passphrase](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
  
 ![Icona della cartella file piccola](../../integration-services/media/filefolder-small.gif "Icona della cartella file piccola") **Autorizzazione: Cosa potete fare?**  
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
  
-   [Mascheramento dati dinamici](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)  
  
-   [Oggetti firmati](/sql/t-sql/statements/add-signature-transact-sql)  
  
 ![Icona della cartella file piccola](../../integration-services/media/filefolder-small.gif "Icona della cartella file piccola") **Sicurezza della connessione: Limitazione e sicurezza**  
 **Protezione con firewall**  
  
-   [Configurazione di Windows Firewall per l'accesso al Motore di database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Impostazioni del firewall del database SQL di Azure](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
-   [Impostazioni del firewall dei servizi di Azure](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
 **Crittografia dei dati in transito**  
  
-   [Secure Sockets Layer per il motore di database](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
-   [Secure Sockets Layer per il database SQL](https://msdn.microsoft.com/library/azure/ff394108.aspx)  
  
 ![Icona della cartella file piccola](../../integration-services/media/filefolder-small.gif "Icona della cartella file piccola") **Controllo: Registrazione dell'accesso**  
 **Controllo automatizzato**  
  
-   [SQL Server Audit &#40;Database Engine&#41;](auditing/sql-server-audit-database-engine.md)  
  
-   [Controllo del database SQL](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)  
  
 **Implementazione di controlli personalizzati**  
  
-   Creazione di [DDL Triggers](../triggers/ddl-triggers.md) e di [DML Triggers](../triggers/dml-triggers.md)  
  
 ![Icona della cartella file piccola](../../integration-services/media/filefolder-small.gif "Icona della cartella file piccola") **Conformità**  
 **SQL Server**  
  
-   [Criteri comuni](https://go.microsoft.com/fwlink/?LinkId=616319)  
  
 **Database SQL**  
  
-   [Centro protezione di Microsoft Azure: conformità per funzionalità](https://azure.microsoft.com/support/trust-center/services/)  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza di SQL Server](securing-sql-server.md)   
 [Entità &#40;motore di database&#41;](authentication-access/principals-database-engine.md)   
 [Certificati SQL Server e chiavi simmetriche](sql-server-certificates-and-asymmetric-keys.md)   
 [Crittografia di SQL Server](encryption/sql-server-encryption.md)   
 [Configurazione superficie di attacco](surface-area-configuration.md)   
 [Password complesse](strong-passwords.md)   
 [Proprietà di database TRUSTWORTHY](trustworthy-database-property.md)   
 [Caratteristiche e attività del motore di database](../../database-engine/database-engine-features-and-tasks.md)  
  
  
