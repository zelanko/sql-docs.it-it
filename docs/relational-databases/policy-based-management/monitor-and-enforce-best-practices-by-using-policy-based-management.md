---
title: Monitorare e applicare le procedure consigliate usando la gestione basata su criteri
description: La gestione basata su criteri offre un set di file di criteri che è possibile importare per le procedure consigliate e valuta i criteri rispetto a un set di destinazione che include istanze, oggetti, database e oggetti di database.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54fdfe36da0d590fa2225ab7cc99af640727b000
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557668"
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La gestione basata su criteri consente di monitorare le procedure consigliate per [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce un set di file di criteri che è possibile importare per le procedure consigliate e descrive come valutare i criteri rispetto a un set di destinazione con istanze, oggetti di istanza, database e oggetti di database. Valutare manualmente i criteri, impostare i criteri per la valutazione di un set di destinazioni in base a una pianificazione oppure per la valutazione di un set di destinazioni in base a un evento. Per altre informazioni sulla gestione basata su criteri, vedere [Amministrazione di server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
## <a name="policy-and-rules-for-database-engine"></a>Criteri e regole per il Motore di database  
 La tabella seguente elenca i criteri disponibili con l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le informazioni relative alle regole per le procedure consigliate valutate dai singoli criteri. I criteri vengono archiviati come file XML e devono essere importati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni sull'importazione di criteri, vedere [Importare i criteri della gestione basata su criteri](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md).  
  
|Nome criteri|Regola per le procedure consigliate|  
|-----------------|------------------------|  
|Algoritmo di crittografia a chiavi asimmetriche|[Livello di crittografia delle chiavi asimmetriche](../../relational-databases/policy-based-management/asymmetric-keys-encryption-strength.md)|  
|Percorso di backup e del file di dati|[Posizionamento dei file di backup in dispositivi separati rispetto ai file di database](https://msdn.microsoft.com/library/7039bebb-1f25-4cf3-81f1-393dfb78da12)|  
|Percorso dati e file di log|[Posizionamento di dati e file di log in unità distinte](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)|  
|Chiusura automatica database|[Impostazione dell'opzione di database AUTO_CLOSE su OFF](../../relational-databases/policy-based-management/set-the-auto-close-database-option-to-off.md)|  
|Compattazione automatica database|[Impostazione dell'opzione di database AUTO_SHRINK su OFF](../../relational-databases/policy-based-management/set-the-auto-shrink-database-option-to-off.md)|  
|Regole di confronto del database|[Impostazione delle regole di confronto dei database definiti dall'utente in modo che corrispondano a quelle dei database master e modello](https://msdn.microsoft.com/library/c686446f-dae1-4b05-a3df-837b3422988d)|  
|Verifica pagina di database|[Impostazione dell'opzione di database PAGE_VERIFY su CHECKSUM](../../relational-databases/policy-based-management/set-the-page-verify-database-option-to-checksum.md)|  
|Stato pagine del database|[Verifica del'integrità di un database contenente pagine sospette](../../relational-databases/policy-based-management/check-integrity-of-database-with-suspect-pages.md)|  
|Autorizzazioni Guest|[Autorizzazioni Guest nei database utente](../../relational-databases/policy-based-management/guest-permissions-on-user-databases.md)|  
|Data ultimo backup completato|[Backup obsoleto](../../relational-databases/policy-based-management/outdated-backup.md)|  
|Autorizzazioni server non concesse al ruolo public|[Autorizzazioni server per il ruolo public](../../relational-databases/policy-based-management/server-public-permissions.md)|  
|Sovrapposizione maschera di affinità a 64 bit SQL Server|[Correggere la sovrapposizione delle opzioni affinity mask e affinity I/O mask](../../relational-databases/policy-based-management/correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|Maschera di affinità SQL Server|[Valore predefinito per la maschera di affinità](../../relational-databases/policy-based-management/keep-the-affinity-mask-default-value.md)|  
|Soglia processo bloccato SQL Server|[Aumento o disabilitazione dell'opzione blocked process threshold](../../relational-databases/policy-based-management/increase-or-disable-blocked-process-threshold.md)|  
|Traccia predefinita SQL Server|[File dei log di traccia predefiniti disabilitati](../../relational-databases/policy-based-management/default-trace-log-files-disabled.md)|  
|Blocchi dinamici SQL Server|[Impostazione dell'opzione di configurazione dei blocchi sul valore predefinito](../../relational-databases/policy-based-management/keep-the-locks-configuration-option-default-value.md)|  
|Lightweight Pooling SQL Server|[Disabilitazione di lightweight pooling](../../relational-databases/policy-based-management/disable-lightweight-pooling.md)|  
|Modalità di accesso SQL Server|[Scegliere una modalità di autenticazione](../../relational-databases/security/choose-an-authentication-mode.md)|  
|Massimo grado parallelismo SQL Server|[Impostazione dell'opzione relativa al massimo grado di parallelismo per ottenere prestazioni ottimali](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|Numero massimo thread di lavoro di SQL Server per SQL Server 2000 a 32 bit|[Verificare l'impostazione relativa al numero massimo di thread di lavoro](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Numero massimo thread di lavoro SQL Server per SQL Server 2000 a 64 bit|[Verificare l'impostazione relativa al numero massimo di thread di lavoro](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Numero massimo thread di lavoro SQL Server per SQL Server 2005 e versioni successive|[Verificare l'impostazione relativa al numero massimo di thread di lavoro](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Dimensioni pacchetto di rete SQL Server|[Valore massimo per le dimensioni del pacchetto di rete impostato su 8060 byte](../../relational-databases/policy-based-management/network-packet-size-should-not-exceed-8060-bytes.md)|  
|Scadenza password SQL Server|[Scadenza della password di accesso di SQL server](../../relational-databases/policy-based-management/sql-server-login-password-expiration.md)|  
|Criteri password SQL Server|[Livello di complessità delle password di accesso di SQL Server](../../relational-databases/policy-based-management/sql-server-login-password-strength.md)|  
|Crittografia a chiave simmetrica per database utente|[Chiavi simmetriche nei database utente](../../relational-databases/policy-based-management/symmetric-keys-on-user-databases.md)|  
|Chiave simmetrica per database master|[Chiavi simmetriche nei database di sistema](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|Chiave simmetrica per database di sistema|[Chiavi simmetriche nei database di sistema](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|Database con proprietà trustworthy|[Bit relativo alla proprietà trustworthy](../../relational-databases/policy-based-management/trustworthy-bit.md)|  
|Errore di danneggiamento risorsa disco del cluster in registro eventi di Windows|[Rilevamento dei problemi relativi all'adattatore host SCSI](../../relational-databases/policy-based-management/detect-scsi-host-adapter-issues.md)|  
|Errore di verifica driver di dispositivo in registro eventi di Windows|[Errore di verifica driver dispositivo](../../relational-databases/policy-based-management/device-driver-control-error.md)|  
|Errore di dispositivo non pronto in registro eventi di Windows|[Errore di dispositivo non pronto](../../relational-databases/policy-based-management/device-not-ready-error.md)|  
|Errore registro eventi di Windows - Richiesta I/O non riuscita|[Rilevamento di una richiesta di I/O non riuscita](../../relational-databases/policy-based-management/detect-failed-input-and-output-requests.md)|  
|Registro eventi di Windows - Avviso di ritardo I/O|[Verifica dei problemi di ritardo di I/O nel sottosistema di I/O del disco](../../relational-databases/policy-based-management/check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Errore registro eventi di Windows - Errore di I/O durante errore di pagina hardware|[Errore di I/O durante un errore di pagina hardware](../../relational-databases/policy-based-management/input-and-output-error-during-hard-page-fault.md)|  
|Errore di tentativo di lettura in registro eventi di Windows|[Verifica dei problemi correlati ai tentativi di lettura nel sottosistema di input/output del disco](../../relational-databases/policy-based-management/check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Errore registro eventi di Windows - Timeout I/O sistema di archiviazione|[Timeout di input o output del sistema di archiviazione](../../relational-databases/policy-based-management/storage-system-input-output-time-out.md)|  
|Errore di sistema in registro eventi di Windows|[Errori di sistema imprevisti](../../relational-databases/policy-based-management/unexpected-system-failures.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo della copia di facet della gestione basata su criteri](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)  
  
  
