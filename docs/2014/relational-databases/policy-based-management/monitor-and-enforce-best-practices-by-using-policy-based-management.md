---
title: Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bfc7cc16c9751ebdf64a8e9cd110547255c944ee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62626048"
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri
  La gestione basata su criteri consente di monitorare le [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]procedure consigliate per. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fornisce un set di file di criteri che è possibile importare come criteri per procedure consigliate e quindi valutare i criteri rispetto a un set di destinazioni che include istanze, oggetti di istanza, database o oggetti di database. È possibile valutare manualmente i criteri, impostare i criteri per la valutazione di un set di destinazioni in base a una pianificazione oppure per la valutazione di un set di destinazioni in base a un evento. Per altre informazioni sulla gestione basata su criteri, vedere [Amministrazione di server tramite la gestione basata su criteri](administer-servers-by-using-policy-based-management.md).  
  
## <a name="policy-and-rules-for-database-engine"></a>Criteri e regole per il Motore di database  
 Nella tabella seguente sono elencati i criteri inclusi nell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e vengono fornite informazioni sulle regole per le procedure consigliate valutate da ciascun criterio. I criteri vengono archiviati come file XML e devono essere importati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni sull'importazione di criteri, vedere [Importare i criteri della gestione basata su criteri](import-a-policy-based-management-policy.md).  
  
|Nome criteri|Regola per le procedure consigliate|  
|-----------------|------------------------|  
|Algoritmo di crittografia a chiavi asimmetriche|[Livello di crittografia delle chiavi asimmetriche](asymmetric-keys-encryption-strength.md)|  
|Percorso di backup e del file di dati|[Posizionamento dei file di backup in dispositivi separati rispetto ai file di database](../../database-engine/backup-files-must-be-on-separate-devices-from-the-database-files.md)|  
|Percorso dati e file di log|[Posizionamento di dati e file di log in unità distinte](place-data-and-log-files-on-separate-drives.md)|  
|Chiusura automatica database|[Impostazione dell'opzione di database AUTO_CLOSE su OFF](set-the-auto-close-database-option-to-off.md)|  
|Compattazione automatica database|[Impostazione dell'opzione di database AUTO_SHRINK su OFF](set-the-auto-shrink-database-option-to-off.md)|  
|Regole di confronto del database|[Impostazione delle regole di confronto dei database definiti dall'utente in modo che corrispondano a quelle dei database master e modello](../../database-engine/set-collation-user-defined-databases-match-master-model-databases.md)|  
|Verifica pagina di database|[Impostazione dell'opzione di database PAGE_VERIFY su CHECKSUM](set-the-page-verify-database-option-to-checksum.md)|  
|Stato pagine del database|[Verifica del'integrità di un database contenente pagine sospette](check-integrity-of-database-with-suspect-pages.md)|  
|Autorizzazioni Guest|[Autorizzazioni Guest nei database utente](guest-permissions-on-user-databases.md)|  
|Data ultimo backup completato|[Backup obsoleto](outdated-backup.md)|  
|Autorizzazioni server non concesse al ruolo public|[Autorizzazioni server per il ruolo public](server-public-permissions.md)|  
|Sovrapposizione maschera di affinità a 32 bit SQL Server|[Correzione della sovrapposizione della maschera di affinità e della maschera di output di input affinità](correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|Sovrapposizione maschera di affinità a 64 bit SQL Server|[Correzione della sovrapposizione della maschera di affinità e della maschera di output di input affinità](correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|Maschera di affinità SQL Server|[Valore predefinito per la maschera di affinità](keep-the-affinity-mask-default-value.md)|  
|Soglia processo bloccato SQL Server|[Aumento o disabilitazione dell'opzione blocked process threshold](increase-or-disable-blocked-process-threshold.md)|  
|Traccia predefinita SQL Server|[File dei log di traccia predefiniti disabilitati](default-trace-log-files-disabled.md)|  
|Blocchi dinamici SQL Server|[Impostazione dell'opzione di configurazione dei blocchi sul valore predefinito](keep-the-locks-configuration-option-default-value.md)|  
|Lightweight Pooling SQL Server|[Disabilitazione di lightweight pooling](disable-lightweight-pooling.md)|  
|Modalità di accesso SQL Server|[Scegliere una modalità di autenticazione](../security/choose-an-authentication-mode.md)|  
|Massimo grado parallelismo SQL Server|[Impostazione dell'opzione relativa al massimo grado di parallelismo per ottenere prestazioni ottimali](set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|Numero massimo thread di lavoro di SQL Server per SQL Server 2000 a 32 bit|[Verifica dell'impostazione relativa al numero massimo di thread di lavoro](verify-max-worker-threads-setting.md)|  
|Numero massimo thread di lavoro SQL Server per SQL Server 2000 a 64 bit|[Verifica dell'impostazione relativa al numero massimo di thread di lavoro](verify-max-worker-threads-setting.md)|  
|Numero massimo thread di lavoro SQL Server per SQL Server 2005 e versioni successive|[Verifica dell'impostazione relativa al numero massimo di thread di lavoro](verify-max-worker-threads-setting.md)|  
|Dimensioni pacchetto di rete SQL Server|[Valore massimo per le dimensioni del pacchetto di rete impostato su 8060 byte](network-packet-size-should-not-exceed-8060-bytes.md)|  
|Scadenza password SQL Server|[Scadenza della password di accesso di SQL server](sql-server-login-password-expiration.md)|  
|Criteri password SQL Server|[Livello di complessità delle password di accesso di SQL Server](sql-server-login-password-strength.md)|  
|Crittografia a chiave simmetrica per database utente|[Chiavi simmetriche nei database utente](symmetric-keys-on-user-databases.md)|  
|Chiave simmetrica per database master|[Chiavi simmetriche nei database di sistema](symmetric-keys-on-system-databases.md)|  
|Chiave simmetrica per database di sistema|[Chiavi simmetriche nei database di sistema](symmetric-keys-on-system-databases.md)|  
|Database con proprietà trustworthy|[Bit relativo alla proprietà trustworthy](trustworthy-bit.md)|  
|Errore di danneggiamento risorsa disco del cluster in registro eventi di Windows|[Rilevamento dei problemi relativi all'adattatore host SCSI](detect-scsi-host-adapter-issues.md)|  
|Errore di verifica driver di dispositivo in registro eventi di Windows|[Errore di verifica driver dispositivo](device-driver-control-error.md)|  
|Errore di dispositivo non pronto in registro eventi di Windows|[Errore di dispositivo non pronto](device-not-ready-error.md)|  
|Errore registro eventi di Windows - Richiesta I/O non riuscita|[Rileva richiesta output di input non riuscita](detect-failed-input-and-output-requests.md)|  
|Registro eventi di Windows - Avviso di ritardo I/O|[Verifica dei problemi di ritardo di I/O nel sottosistema di I/O del disco](check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Errore registro eventi di Windows - Errore di I/O durante errore di pagina hardware|[Errore di I/O durante un errore di pagina hardware](input-and-output-error-during-hard-page-fault.md)|  
|Errore di tentativo di lettura in registro eventi di Windows|[Verifica dei problemi relativi ai tentativi di lettura nel sottosistema di input/output del disco](check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Errore registro eventi di Windows - Timeout I/O sistema di archiviazione|[Timeout di input o output del sistema di archiviazione](storage-system-input-output-time-out.md)|  
|Errore di sistema in registro eventi di Windows|[Errori di sistema imprevisti](unexpected-system-failures.md)|  
  
## <a name="see-also"></a>Vedi anche  
 [Utilizzo della copia di facet della gestione basata su criteri](working-with-policy-based-management-facets.md)  
  
  
