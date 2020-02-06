---
title: Use Built-in Security in Windows SharePoint Services for Report Server Items | Microsoft Docs (Usare la sicurezza predefinita di Windows SharePoint Services per gli elementi del server di report | Microsoft Docs)
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 9577e88d-c22b-4934-936f-e0f1400cedf5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d57768a580b4343fbe1e6ee2919a8161013371a4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65579415"
---
# <a name="use-built-in-security-in-windows-sharepoint-services-for-report-server-items"></a>Utilizzare la sicurezza predefinita di Windows SharePoint Services per gli elementi del server di report
  In SharePoint sono disponibili funzionalità di sicurezza predefinite che è possibile utilizzare per accedere agli elementi del server di report da siti e raccolte di SharePoint. Se sono già state assegnate autorizzazioni per siti ed elenchi agli utenti, questi ultimi potranno accedere alle operazioni e agli elementi del server di report subito dopo la configurazione delle impostazioni per l'integrazione tra SharePoint e un server di report.  
  
## <a name="securable-items"></a>Elementi a sicurezza diretta  
 Le autorizzazioni definite per un sito o una raccolta possono essere utilizzate per concedere l'accesso agli elementi del server di report. Se tuttavia si desidera proteggere singoli elementi, sarà possibile impostare autorizzazioni per i tipi di contenuto seguenti:  
  
|Tipo file|Descrizione|  
|---------------|-----------------|  
|rdl|File di definizione del report. Specifica il layout del report e i comandi utilizzati per recuperare i dati. Un file di definizione del report utilizza le informazioni di connessione all'origine dati per recuperare i dati durante l'elaborazione del report. Se il file definisce un report ad hoc creato in Generatore report, a tale report sarà associato un file modello (con estensione smdl), il quale determina l'impostazione dell'ambito di esplorazione dei dati nel report visualizzabile.|  
|smdl|File modello di report che descrive le strutture di dati e le relative relazioni. Viene utilizzato per creare ed eseguire report di Generatore report.|  
|rsds|File di origine dati condivisa che specifica informazioni per la connessione a un'origine dati esterna. Viene utilizzato dai file di definizione (con estensione rdl) e modello (con estensione smdl) del report. I modelli di report utilizzano sempre file rsds per ottenere informazioni di connessione a un'origine dati sottostante. Le definizioni del report possono utilizzare file rsds oppure informazioni di connessione definite nelle proprietà del report relative alle origini dati.|  
|rsc|File di parte del report che definisce il layout e la struttura di un elemento di report o di un'area dati. Utilizzato per pubblicare la parte del report in un server affinché l'elemento possa essere riutilizzato da altri autori di report dalla Raccolta parti del report.|  
|rsd|File di set di dati condiviso che definisce la sintassi di query e le proprietà per un set di dati. I set di dati condivisi possono essere condivisi, archiviati, elaborati e memorizzati nella cache esternamente a un report.|  
  
 Le pianificazioni, le sottoscrizioni e la cronologia dei report non sono elementi a protezione diretta. È possibile impostare autorizzazioni a livello di sito o raccolta che determinano se uno specifico utente può creare o utilizzare pianificazioni, sottoscrizioni e la cronologia dei report, ma non è possibile proteggere tali elementi direttamente.  
  
 Per proteggere singoli elementi, selezionare l'elemento desiderato nella raccolta, fare clic sulla freccia verso il basso e selezionare **Gestisci autorizzazioni**. Scegliere **Modifica autorizzazioni** dal menu **Azioni**.  
  
## <a name="using-built-in-groups-and-permission-levels-to-access-report-server-items"></a>Utilizzo dei livelli di autorizzazione e dei gruppi incorporati per l'accesso agli elementi di un server di report  
 Se si utilizza l'ereditarietà delle autorizzazioni e i gruppi SharePoint standard, sarà possibile accedere alla maggior parte delle operazioni del server di report subito dopo la configurazione delle impostazioni di integrazione nel server di report e nelle istanze di SharePoint.  
  
 In SharePoint sono disponibili gruppi standard di cui viene eseguito il mapping a livelli di autorizzazione predefiniti che determinano la modalità di accesso a documenti e pagine di un sito di SharePoint. Se si usano i gruppi standard e i livelli di autorizzazione predefiniti, e i siti usati sono configurati per l'ereditarietà delle autorizzazioni, sarà possibile usare le funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] come specificato di seguito:  
  
|**Gruppi di SharePoint**|**Livello di autorizzazione**|**Summary**|**Accesso al server di report**|  
|---------------------------|--------------------------|-----------------|------------------------------|  
|**Proprietari**|Controllo completo|I proprietari dispongono di autorizzazioni complete per la creazione, la gestione e la protezione di operazioni ed elementi del server di report.|Impostazione di autorizzazioni che controllano l'accesso a tutti gli elementi del server di report archiviati nelle raccolte del sito. Impostazione di autorizzazioni all'interno di un modello di report (in questo caso si parla anche di sicurezza degli elementi di un modello). Personalizzazione di una web part Visualizzatore report. Aggiunta di report e altri elementi alle raccolte. Modifica delle proprietà degli elementi per report e altri documenti. Eliminazione di report e altri elementi. Visualizzazione di report, inclusi quelli che utilizzano modelli di report per l'esplorazione dei dati. Impostazione di parametri per i report. Impostazione di opzioni di elaborazione per un report. Generazione di modelli di report. Creazione di report in Generatore report. Creazione e gestione di origini dati condivise. Creazione, modifica ed eliminazione di sottoscrizioni di proprietà di un utente. Creazione e gestione di pianificazioni condivise utilizzate in tutto il sito. Creazione e gestione delle diverse versioni di uno stesso documento, inclusa la cronologia del report. Download del file di origine per una definizione del report o modello di report. Sostituzione di una definizione del report, di un modello di report, di un'origine dati condivisa o di una risorsa senza modificare autorizzazioni e proprietà degli elementi.|  
|**Members**|Contribuire|I membri possono creare nuovi elementi e pubblicare modelli ed elementi di report dagli strumenti di progettazione alle raccolte di SharePoint.|Aggiunta di report e altri elementi alle raccolte. Modifica delle proprietà degli elementi per report e altri documenti. Eliminazione di report e altri elementi. Visualizzazione di report, inclusi quelli che utilizzano modelli di report per l'esplorazione dei dati. Visualizzazione delle versioni precedenti di un documento, inclusi gli snapshot della cronologia del report (l'utente deve disporre anche dell'autorizzazione per l'apertura del report per cui è stata creata la cronologia del report). Impostazione di parametri per i report. Impostazione di opzioni di elaborazione per un report. Generazione di modelli di report. Creazione di report in Generatore report. Creazione e gestione di origini dati condivise. Creazione, modifica ed eliminazione di sottoscrizioni di proprietà dell'utente. Utilizzo di pianificazioni condivise con una sottoscrizione. Creazione e gestione delle diverse versioni di uno stesso documento, inclusa la cronologia del report. Download del file di origine per una definizione del report o modello di report. Sostituzione di una definizione del report, di un modello di report, di un'origine dati condivisa o di una risorsa senza modificare autorizzazioni e proprietà degli elementi.|  
|**Visitatori** e **Visualizzatori**|Lettura|I visitatori possono visualizzare i report|Visualizzazione di report, inclusi quelli che utilizzano modelli di report per l'esplorazione dei dati.|  
  
 Se non si utilizzano i livelli di autorizzazione e i gruppi incorporati, per accedere alle funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sarà necessario includere autorizzazioni specifiche. Per altre informazioni, vedere [Impostare le autorizzazioni per le operazioni del server di report in un'applicazione Web di SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Confrontare ruoli e attività di Reporting Services con autorizzazioni e gruppi di SharePoint](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Impostare le autorizzazioni per le operazioni del server di report in un'applicazione Web di SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
