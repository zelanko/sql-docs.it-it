---
title: Concetti di Data Quality Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 837c71ee-48fa-4044-8744-2be9119aaa04
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6f1cba6a6a20fc804d29aeb0dbf43d7bebfbb225
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154450"
---
# <a name="data-quality-services-concepts"></a>Concetti di Data Quality Services
  In questo argomento viene fornito un breve riepilogo dei concetti di [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) nell'ambito della gestione delle informazioni, dei progetti Data Quality e dell'amministrazione della qualità dei dati.  
  
##  <a name="Knowledge"></a> Concetti relativi alla gestione delle informazioni  
 La Knowledge Base DQS è un repository di metadati creati dall'amministratore dei dati o dal personale IT da utilizzare per migliorare la qualità dei dati tramite la pulizia e la corrispondenza dei dati. La gestione delle informazioni DQS include i processi utilizzati per creare e gestire la Knowledge Base, sia in modo computerizzato che in modo interattivo.  
  
 **Individuazione informazioni**  
  
 L'individuazione delle informazioni è un processo computerizzato che analizza esempi di dati dell'organizzazione per compilare le informazioni sui dati. Una volta ottenuti i risultati dell'analisi, è possibile convalidare e migliorare le informazioni, quindi applicarle per eseguire la pulizia dei dati, la corrispondenza e il profiling. Per altre informazioni, vedere [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Gestione dominio**  
  
 Il processo di gestione del dominio consente di modificare o aumentare le informazioni generate dal processo di individuazione delle informazioni. È possibile modificare, aggiornare e rivedere in modo interattivo le informazioni in una Knowledge Base. Una Knowledge Base è costituita da domini di dati che contengono i valori di dominio e il relativo stato, le regole di dominio, le relazioni basate su termini e i dati di riferimento. Nella gestione del dominio è possibile modificare le proprietà del dominio, associare i dati di riferimento a un dominio, gestire le regole di dominio, gestire i valori di dominio e immettere le relazioni di dati nonché creare, eliminare, importare o esportare i domini. È inoltre possibile utilizzare domini compositi che aggregano più domini singoli. Per altre informazioni, vedere [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Criteri di abbinamento**  
  
 I criteri di corrispondenza contengono le regole di corrispondenza utilizzate per eseguire la deduplicazione dei dati. Il processo dei criteri di corrispondenza consente di creare le regole di corrispondenza, di ottimizzarle in base ai risultati corrispondenti e ai dati di profiling e di aggiungere i criteri alla Knowledge Base. Per altre informazioni, vedere [Corrispondenza di dati](../../2014/data-quality-services/data-matching.md).  
  
 **Servizi dati di riferimento**  
  
 È possibile utilizzare i dati di riferimento per convalidare, correggere e migliorare i dati, sfruttando i servizi di società che garantiscono la qualità dei dati di riferimento. È possibile usare i servizi di Azure Marketplace per connettersi ai provider di dati di riferimento oppure è possibile usare una connessione diretta a un provider. Per altre informazioni, vedere [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md).  
  
 Per ulteriori informazioni sulla gestione delle informazioni in DQS, vedere [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
##  <a name="Projects"></a> Concetti relativi ai progetti Data Quality  
 L'amministratore dei dati esegue le operazioni di qualità dei dati (pulizia e corrispondenza) utilizzando un progetto Data Quality nell'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
 **Pulizia dei dati**  
  
 La pulizia dei dati in DQS viene effettuata in base alle informazioni incluse nella Knowledge Base DQS e prevede un processo in due passaggi:  
  
-   **Pulizia assistita da computer**: DQS usa le informazioni disponibili nella Knowledge Base selezionata per la pulizia, al fine di proporre correzioni e suggerimenti relativi ai valori in un'origine dati.  
  
-   **Pulizia interattiva**: l'amministratore dei dati può eseguire il processo di pulizia interattiva per modificare o aumentare le correzioni dei dati proposte dal processo di pulizia dei dati assistito da computer. L'amministratore dei dati esegue questa operazione utilizzando livelli di confidenza e statistiche identificati dal processo di pulizia dei dati o immettendo manualmente le proprie modifiche nel progetto.  
  
 In seguito al processo di pulizia, l'amministratore può esportare i dati elaborati in un database di SQL Server, un file con estensione csv o un file di Excel. Per altre informazioni, vedere [Data Cleansing](../../2014/data-quality-services/data-cleansing.md).  
  
 **Corrispondenza di dati**  
  
 Con il processo di corrispondenza l'amministratore dei dati può confrontare i dati in modo da poter allineare quelli simili tramite il processo di deduplicazione. La deduplicazione in DQS viene eseguita in base alle regole di corrispondenza contenute nella Knowledge Base. L'amministratore dei dati specifica i parametri per il processo di corrispondenza all'interno di un progetto Data Quality. Per altre informazioni, vedere [Data Matching](../../2014/data-quality-services/data-matching.md).  
  
 **Profiling e notifiche**  
  
 Con il profiling dei dati, agli amministratori dei dati vengono fornite statistiche e informazioni in tempo reale sui dati elaborati da DQS per le attività di pulizia e di corrispondenza durante l'esecuzione di un progetto Data Quality. Viene inoltre valutata l'efficacia delle attività di pulizia e di corrispondenza in un progetto Data Quality e, con le notifiche, l'utente può scegliere le azioni che possono essere eseguite per migliorare le attività di pulizia e di corrispondenza dei dati. Per altre informazioni, vedere [Data Profiling and Notifications in DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
 Per altre informazioni sui progetti Data Quality in DQS, vedere [Progetti Data Quality &#40;DQS&#41;](../../2014/data-quality-services/data-quality-projects-dqs.md).  
  
##  <a name="Admin"></a> Concetti relativi all'amministrazione della qualità dei dati  
 Un amministratore DQS può eseguire numerose attività amministrative mediante l'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
 **Monitoraggio attività**  
  
 Tramite il monitoraggio delle attività viene visualizzato lo stato di ogni attività eseguita all'interno di un intervallo di dati, vengono forniti i dati per ogni attività e viene consentito agli amministratori DQS di controllare un'attività. Per altre informazioni, vedere [Monitor DQS Activities](../../2014/data-quality-services/monitor-dqs-activities.md).  
  
 **Configurazione**  
  
 Con l'opzione Configurazione è possibile effettuare le operazioni seguenti:  
  
-   Configurare le impostazioni del servizio dati di riferimento. Per altre informazioni, vedere [Configure DQS to Use Reference Data](../../2014/data-quality-services/configure-dqs-to-use-reference-data.md).  
  
-   Impostare i valori soglia per le attività di pulizia e di corrispondenza. Per altre informazioni, vedere [Configurazione dei valori soglia per le attività di pulizia e di individuazione delle corrispondenze](../../2014/data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   Abilitare o disabilitare le notifiche di profiling Per altre informazioni, vedere [Abilitare o disabilitare le notifiche di profiling in DQS](../../2014/data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md).  
  
-   Configurare i livelli di gravità per i file di log DQS a livello di attività o a livello di modulo, che rappresenta la modalità più avanzata. Per altre informazioni, vedere [Configure Severity Levels for DQS Log Files](../../2014/data-quality-services/configure-severity-levels-for-dqs-log-files.md).  
  
 **Sicurezza relativa a DQS**  
  
 È possibile utilizzare i ruoli all'interno del meccanismo di sicurezza di SQL Server per proteggere DQS. Sono disponibili tre ruoli DQS tramite cui viene determinato il livello di accesso per un utente nell'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , cioè dqs_administrator, dqs_kb_editor e dqs_kb_operator. Non è possibile concedere ruoli agli utenti utilizzando l'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , bensì mediante SQL Server Management Studio. Per altre informazioni, vedere [DQS Security](../../2014/data-quality-services/dqs-security.md).  
  
 Per ulteriori informazioni sull'amministrazione DQS, vedere [DQS Administration](../../2014/data-quality-services/dqs-administration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Data Quality Services](../../2014/data-quality-services/data-quality-services.md)  
  
  
