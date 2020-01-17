---
title: Documentazione sulla sicurezza per SQL Server e il database SQL di Azure
description: Riferimento ai contenuti relativi a sicurezza e protezione per SQL Server e il database SQL di Azure.
ms.custom: seo-lt-2019
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9bf5e128b054bbea218c6b791666f5698c24c37d
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557706"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>Centro di sicurezza per il motore di database di SQL Server e il database SQL di Azure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In questa pagina vengono forniti i collegamenti che consentono di trovare informazioni su sicurezza e protezione nel [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 **Legenda**  
  
 ![security-center-legend](../performance/media/security-center-legend.PNG "security-center-legend")  
  
##  <a name="Who"></a> Autenticazione: informazioni sull'utente  
  
|||  
|-|-|  
|**Scelta del tipo di autenticazione**<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Autenticazione di Windows<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref3::|") Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb")  Azure Active Directory|Scelta del tipo di autenticazione (Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])<br /><br /> [Scegliere una modalità di autenticazione](../../relational-databases/security/choose-an-authentication-mode.md)<br /><br /> [Connettersi al Database SQL utilizzando l’autenticazione di Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)|  
|**Dove viene eseguita l'autenticazione**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref5::|") Database master: account di accesso e utenti di database<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref6::|") Database utente: utenti di database contenuti|Autenticazione a livello di database master (account di accesso e utenti di database)<br /><br /> [Creazione di un account di accesso di SQL Server](../../relational-databases/security/authentication-access/create-a-login.md)<br /><br /> [Gestione di database e account di accesso in database SQL di Azure](https://msdn.microsoft.com/library/ee336235.aspx)<br /><br /> [Creazione di un utente di database](../../relational-databases/security/authentication-access/create-a-database-user.md)<br /><br /> <br /><br /> Autenticazione a livello di database utente<br /><br /> [Utenti di database indipendente: rendere portabile un database](../../relational-databases/security/contained-database-users-making-your-database-portable.md)|  
|**Uso di altre identità**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref7::|") Credenziali<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "|::ref8::|") Esecuzione con un altro account di accesso<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref9::|") Esecuzione con un altro utente di database|[Credenziali &#40;motore di database&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)<br /><br /> [Esecuzione con un altro account di accesso](../../t-sql/statements/execute-as-transact-sql.md)<br /><br /> [Esecuzione con un altro utente di database](../../t-sql/statements/execute-as-transact-sql.md)|  
  
##  <a name="What"></a> Autorizzazione: operazioni consentite  
  
|||  
|-|-|  
|**Concessione, revoca e negazione delle autorizzazioni**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref10::|") Classi a protezione diretta<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "|::ref11::|") Autorizzazioni server granulari<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref12::|") Autorizzazioni di database granulari|[Gerarchia delle autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)<br /><br /> [Autorizzazioni](../../relational-databases/security/permissions-database-engine.md)<br /><br /> [Entità a protezione diretta](../../relational-databases/security/securables.md)<br /><br /> [Introduzione alle autorizzazioni del motore di database](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)|  
|**Sicurezza in base ai ruoli**<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "|::ref13::|") Ruoli a livello di server<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref14::|") Ruoli a livello di database|[Ruoli a livello di server](../../relational-databases/security/authentication-access/server-level-roles.md)<br /><br /> [Ruoli a livello di database](../../relational-databases/security/authentication-access/database-level-roles.md)|  
|**Limitazione dell'accesso ai dati agli elementi di dati selezionati**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref15::|") Limitare l'accesso ai dati con viste/stored procedure<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref16::|") Sicurezza a livello di riga<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref17::|") Mascheramento dati dinamici<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref18::|") Oggetti firmati|Uso di [viste](../../relational-databases/views/views.md) e [routine](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)per limitare l'accesso ai dati<br /><br /> [Sicurezza a livello di riga (SQL Server)](../../relational-databases/security/row-level-security.md)<br /><br /> [Sicurezza a livello di riga (Database SQL di Azure)](https://msdn.microsoft.com/library/azure/dn765131.aspx)<br /><br /> [Mascheramento dati dinamici (SQL Server)](../../relational-databases/security/dynamic-data-masking.md)<br /><br /> [Mascheramento dati dinamici (Database SQL di Azure)](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [Oggetti firmati](../../t-sql/statements/add-signature-transact-sql.md)|  
  
##  <a name="Encrypt"></a> Crittografia: archiviazione di dati segreti  
  
|||  
|-|-|  
|**Crittografia dei file**<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "|::ref19::|") Crittografia BitLocker (a livello di unità)<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "|::ref20::|") Crittografia NTFS (a livello di cartella)<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref21::|") Transparent Data Encryption (a livello di file)<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref22::|") Crittografia dei backup (a livello di file)|[BitLocker (a livello di unità)](https://support.microsoft.com/kb/2855131)<br /><br /> [Crittografia NTFS (a livello di cartella)](https://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [Transparent Data Encryption (a livello di file)](../../relational-databases/security/encryption/transparent-data-encryption.md)<br /><br /> [Crittografia dei backup (a livello di file)](../../relational-databases/backup-restore/backup-encryption.md)|  
|**Crittografia delle origini**<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "|::ref23::|") Modulo Extensible Key Management<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "|::ref24::|") Chiavi archiviate nell'insieme di credenziali di Azure<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref25::|") Always Encrypted|[Modulo Extensible Key Management](../../relational-databases/security/encryption/extensible-key-management-ekm.md)<br /><br /> [Chiavi archiviate nell'insieme di credenziali di Azure](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)<br /><br /> [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)|  
|**Crittografia di colonne, dati e chiavi**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref26::|") Crittografia mediante certificato<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref27::|") Crittografia mediante chiave simmetrica<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref28::|") Crittografia mediante chiave asimmetrica<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref29::|") Crittografia mediante passphrase|[Crittografia mediante certificato](../../t-sql/functions/encryptbycert-transact-sql.md)<br /><br /> [Crittografia mediante chiave asimmetrica](../../t-sql/functions/encryptbyasymkey-transact-sql.md)<br /><br /> [Crittografia mediante chiave simmetrica](../../t-sql/functions/encryptbykey-transact-sql.md)<br /><br /> [Crittografia mediante passphrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md)<br /><br /> [Crittografia di una colonna di dati](../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
##  <a name="Connect"></a> Sicurezza della connessione: limitazioni e protezione  
  
|||  
|-|-|  
|**Protezione con firewall**<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "|::ref30::|") Impostazioni di Windows Firewall<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "|::ref31::|") Impostazioni del firewall dei servizi di Azure<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "|::ref32::|") Impostazioni del firewall del database|[Configurare Windows Firewall per l'accesso al motore di database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)<br /><br /> [Impostazioni del firewall del database SQL di Azure](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)<br /><br /> [Impostazioni del firewall dei servizi di Azure](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)|  
|**Crittografia dei dati in transito**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "|::ref33::|") Connessioni SSL forzate<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "|::ref34::|") Connessioni SSL facoltative|[Secure Sockets Layer per il motore di database](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)<br /><br /> [Secure Sockets Layer per il database SQL](https://msdn.microsoft.com/library/azure/ff394108.aspx)<br /><br /> [Supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/kb/3135244)|  
  
##  <a name="Audit"></a> Controllo: registrazione dell'accesso  
  
|||  
|-|-|  
|**Controllo automatizzato**<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref35::|") [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Controllo (livello di server e database)<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "|::ref36::|") [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Controllo (livello di database)<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") Rilevamento minacce| <br /><br /> [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)<br /><br /> [Controllo del database SQL](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> [Introduzione ad Advanced Threat Protection per il database SQL](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/) <br /><br /> [Valutazione delle vulnerabilità del database SQL](https://docs.microsoft.com/azure/sql-database/sql-vulnerability-assessment) |  
|**Controllo personalizzato**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "|::ref38::|") Trigger|Implementazione di controlli personalizzati: Creazione di [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md) e di [DML Triggers](../../relational-databases/triggers/dml-triggers.md)|  
|**Conformità**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "|::ref39::|") Conformità|SQL Server:<br />                        [Criteri comuni](https://go.microsoft.com/fwlink/?LinkId=616319)<br /><br /> Database SQL:<br />                        [Centro protezione di Microsoft Azure: conformità per funzionalità](https://azure.microsoft.com/support/trust-center/services/)|  
  
##  <a name="SQLInjection"></a> Attacco intrusivo nel codice SQL  
 In un attacco SQL injection il malware viene inserito in stringhe successivamente passate al [!INCLUDE[ssDE](../../includes/ssde-md.md)] per l'analisi e l'esecuzione. Per la prevenzione degli attacchi di questo tipo è necessario esaminare tutte le procedure che creano istruzioni SQL, poiché in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono eseguite tutte le query sintatticamente valide ricevute. Tutti i sistemi di database sono a rischio di attacchi SQL injection e molte delle vulnerabilità vengono introdotte nell'applicazione che sta eseguendo una query sul [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Per contrastare gli attacchi SQL injection è possibile usare stored procedure e comandi con parametri, evitando l'SQL dinamico e limitando le autorizzazioni per tutti gli utenti.  Per altre informazioni, vedere [Attacco intrusivo nel codice SQL](../../relational-databases/security/sql-injection.md).  
  
 Collegamenti aggiuntivi per i programmatori di applicazioni:  
  
-   [Scenari di sicurezza delle applicazioni in SQL Server](/dotnet/framework/data/adonet/sql/application-security-scenarios-in-sql-server)  
  
-   [Scrittura di istruzioni SQL dinamiche protette in SQL Server](/dotnet/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server)  
  
-   [Procedura: Proteggere da attacchi SQL injection in ASP.NET](https://msdn.microsoft.com/library/ff648339.aspx)  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alle autorizzazioni del motore di database](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Sicurezza di SQL Server](../../relational-databases/security/securing-sql-server.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Certificati SQL Server e chiavi simmetriche](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)   
 [Crittografia di SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Configurazione superficie di attacco](../../relational-databases/security/surface-area-configuration.md)   
 [Password complesse](../../relational-databases/security/strong-passwords.md)   
 [Proprietà di database TRUSTWORTHY](../../relational-databases/security/trustworthy-database-property.md)   
 [Caratteristiche e attività del motore di database](https://msdn.microsoft.com/library/d9efe145-3306-4d61-bd77-e2af43e19c34)  
 [Protezione della proprietà intellettuale di SQL Server](../../relational-databases/security/protecting-your-sql-server-intellectual-property.md)   
  
[!INCLUDE[get-help-security](../../includes/get-help-security.md)]
