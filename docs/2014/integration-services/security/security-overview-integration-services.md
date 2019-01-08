---
title: Panoramica sulla sicurezza (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- Integration Services, security
- security [Integration Services], about security
- passwords [Integration Services]
- packages [Integration Services], security
- SQL Server Integration Services, security
- SSIS, security
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 01aa0b88-d477-4581-9a3b-2efc3de2b133
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 35376c36361bd7453ed925c8b0be5721aa120037
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761203"
---
# <a name="security-overview-integration-services"></a>Panoramica sulla sicurezza (Integration Services)
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] la sicurezza è costituita da diversi livelli che forniscono un ambiente di sicurezza protetto e flessibile. Questi livelli di sicurezza includono l'uso di firme digitali, proprietà dei pacchetti, ruoli di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e autorizzazioni del sistema operativo. La maggior parte di queste caratteristiche di sicurezza rientra nelle categorie di identità e di controllo dell'accesso.  
  
## <a name="identity-features"></a>Caratteristiche di identità  
 Implementando le caratteristiche di identità nei pacchetti, è possibile raggiungere l'obiettivo seguente:  
  
 **Aprire ed eseguire i pacchetti solo da origini attendibili**.  
  
 Per aprire ed eseguire i pacchetti solo da origini attendibili, è necessario identificare innanzitutto l'origine dei pacchetti. È possibile identificare l'origine dei pacchetti tramite la firma con certificati. Quando si aprono o si eseguono i pacchetti, è possibile impostare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in modo che verifichi la presenza e la validità delle firme digitali. Per altre informazioni, vedere [Identificazione dell'origine dei pacchetti con firme digitali](identify-the-source-of-packages-with-digital-signatures.md).  
  
## <a name="access-control-features"></a>Caratteristiche di controllo dell'accesso  
 Implementando le caratteristiche di identità nei pacchetti, è possibile raggiungere l'obiettivo seguente:  
  
 **Assicurarsi che i pacchetti vengano aperti ed eseguiti solo da utenti autorizzati**.  
  
 Per assicurarsi che i pacchetti vengano aperti ed eseguiti solo da utenti autorizzati, è necessario controllare l'accesso alle informazioni seguenti:  
  
-   Controllare l'accesso al contenuto dei pacchetti, soprattutto ai dati sensibili.  
  
-   Controllare l'accesso ai pacchetti e alle configurazioni dei pacchetti archiviate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Controllare l'accesso ai pacchetti e ai file correlati, quali configurazioni, log e file di checkpoint, archiviati nel file system.  
  
-   Controllare l'accesso al servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e alle informazioni sui pacchetti visualizzate dal servizio in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="controlling-access-to-the-contents-of-packages"></a>Controllo dell'accesso al contenuto dei pacchetti  
 Per limitare l'accesso al contenuto di un pacchetto, è possibile crittografare i pacchetti impostando la proprietà ProtectionLevel del pacchetto. Questa proprietà può essere impostata sul livello di protezione richiesto dal pacchetto. Ad esempio, nell'ambiente di sviluppo di un gruppo di lavoro è possibile crittografare un pacchetto impostando una password nota solo ai membri del gruppo che lavorano al pacchetto.  
  
 Quando si imposta la proprietà ProtectionLevel di un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] individua automaticamente le proprietà riservate e le gestisce in base al livello di protezione pacchetto specificato. Impostare ad esempio la proprietà ProtectionLevel per un pacchetto su un livello che crittografa le informazioni riservate con una password. Per questo pacchetto, in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] vengono crittografati automaticamente i valori di tutte le proprietà riservate e i dati corrispondenti verranno visualizzati solo se viene fornita la password corretta.  
  
 In genere, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] identifica le proprietà come riservate se contengono informazioni, ad esempio una password o una stringa di connessione, o se corrispondono a variabili o a nodi XML generati dall'attività. In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] una proprietà viene considerata riservata a seconda se lo sviluppatore del componente di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , ad esempio una gestione connessione o un'attività, abbia definito la proprietà come riservata. Gli utenti non possono aggiungere proprietà all'elenco di proprietà considerate riservate, né possono rimuoverle. Se si scrivono attività, gestioni connessione o componenti del flusso di dati personalizzati, è possibile specificare le proprietà che devono essere considerate riservate in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Per altre informazioni, vedere [Access Control for Sensitive Data in Packages](access-control-for-sensitive-data-in-packages.md).  
  
### <a name="controlling-access-to-packages"></a>Controllo dell'accesso ai pacchetti  
 I pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] possono essere salvati nel database msdb in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o nel file system come file XML con estensione dtsx. Per altre informazioni, vedere [Salvataggio di pacchetti](../save-packages.md).  
  
#### <a name="saving-packages-to-the-msdb-database"></a>Salvataggio dei pacchetti nel database msdb  
 Con il salvataggio dei pacchetti nel database msdb la sicurezza viene implementata a livello di server, di database e di tabella. Nel database msdb i pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] vengono archiviati nella tabella sysssispackages. Poiché i pacchetti vengono salvati nelle tabelle sysssispackages e sysdtspackages del database msdb, quando si esegue il backup del database msdb automaticamente viene eseguito il backup dei pacchetti.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - I pacchetti archiviati nel database msdb possono essere protetti anche applicando i ruoli a livello di database di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include i tre ruoli predefiniti a livello di database db_ssisadmin, db_ssisltduser e db_ssisoperator per il controllo dell'accesso ai pacchetti. A ogni pacchetto è possibile associare un ruolo di lettore e un ruolo di scrittore. È inoltre possibile definire ruoli personalizzati a livello di database da usare nei pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . I ruoli possono essere implementati solo nei pacchetti salvati nel database msdb in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Ruoli Integration Services &#40;servizio SSIS&#41;](integration-services-roles-ssis-service.md).  
  
#### <a name="saving-packages-to-the-file-system"></a>Salvataggio di pacchetti nel file system  
 Se i pacchetti vengono archiviati nel file system anziché nel database msdb, è necessario proteggere i file di pacchetto e le cartelle che li contengono.  
  
### <a name="controlling-access-to-files-used-by-packages"></a>Controllo dell'accesso ai file utilizzati dai pacchetti  
 I pacchetti configurati per l'utilizzo di configurazioni, checkpoint e registrazione generano informazioni che vengono archiviate all'esterno dei pacchetti stessi. Tali informazioni potrebbero essere riservate e devono essere pertanto protette. I file di checkpoint possono essere salvati solo nel file system, mentre le configurazione e i log possono essere salvati sia nel file system che nelle tabelle di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Le configurazioni e i log salvati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono protetti tramite la sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma per le informazioni scritte ne file system è necessario implementare livelli di sicurezza aggiuntivi.  
  
 Per altre informazioni, vedere [Accesso ai file utilizzati dai pacchetti](../access-to-files-used-by-packages.md).  
  
#### <a name="storing-package-configurations-securely"></a>Archiviazione sicura delle configurazioni del pacchetto  
 Le configurazioni dei pacchetti possono essere salvate in una tabella in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o nel file system.  
  
 Le configurazioni possono essere salvate in qualsiasi database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , non solo nel database msdb. È quindi possibile specificare quale database utilizzare come repository delle configurazioni dei pacchetti. È inoltre possibile specificare il nome della tabella in cui includere le configurazioni, la quale verrà creata automaticamente in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con la struttura corretta. Con il salvataggio delle configurazioni in una tabella la sicurezza viene implementata a livello di server, di database e di tabella. Inoltre, per le configurazioni salvate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito automaticamente il backup quando si esegue il backup del database.  
  
 Se le configurazioni vengono archiviate nel file system anziché in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario proteggere le cartelle contenenti i file di configurazione dei pacchetti.  
  
 Per ulteriori informazioni sulle configurazioni, vedere [Package Configurations](../package-configurations.md).  
  
### <a name="controlling-access-to-the-integration-services-service"></a>Controllo dell'accesso al servizio Integration Services  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] l'elenco dei pacchetti archiviati viene visualizzato tramite il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per impedire agli utenti non autorizzati di visualizzare informazioni sui pacchetti archiviati in computer locali e remoti, acquisendo quindi informazioni private, limitare l'accesso ai computer in cui viene eseguito il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per altre informazioni, vedere [Accesso al servizio Integration Services](../access-to-the-integration-services-service.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 Nell'elenco seguente sono contenuti collegamenti ad argomenti che illustrano come eseguire un'attività relativa alla sicurezza.  
  
-   [Creazione di un ruolo definito dall'utente](../create-a-user-defined-role.md)  
  
-   [Assegnazione di un ruolo lettura e scrittura a un pacchetto](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Implementazione di criteri per le firme impostando un valore del Registro di sistema](../implement-a-signing-policy-by-setting-a-registry-value.md)  
  
-   [Firma di un pacchetto tramite certificato digitale](../sign-a-package-by-using-a-digital-certificate.md)  
  
-   [Impostazione o modifica del livello di protezione dei pacchetti](../set-or-change-the-protection-level-of-packages.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
