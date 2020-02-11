---
title: Server di report di Reporting Services (modalità nativa) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- administering Reporting Services
- administering [Reporting Services]
- Reporting Services, administration
ms.assetid: fa0d84e2-4c21-432c-aa7c-23517da75253
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3be08f0962b7440d5cd0812ad365a752aa1b89d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66103307"
---
# <a name="reporting-services-report-server-native-mode"></a>Reporting Services Report Server (Native Mode)
  Un server di report configurato per la modalità nativa viene eseguito come server applicazioni che fornisce tutte le funzionalità di elaborazione e gestione esclusivamente tramite i componenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 È possibile utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o Gestione report per gestire [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] i report. Utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per gestire un server di report in modalità nativa.  
  
 Se il server di report è configurato per la modalità SharePoint, è necessario utilizzare le pagine di gestione contenuto nel sito di SharePoint per gestire report, origini dati condivise e altri elementi del server di report.  
  
 In questo argomento sono contenute le informazioni indicate di seguito.  
  
-   [Riepilogo della modalità nativa](#bkmk_sum)  
  
-   [Gestione del contenuto](#bkmk_managecontent)  
  
-   [Sicurezza e gestione di una risorsa](#bkmk_manageresources)  
  
-   [Riferimento a una risorsa immagine da un report](#bkmk_referenceimage)  
  
##  <a name="bkmk_sum"></a>Riepilogo della modalità nativa  
 Un'installazione in modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è costituita da diverse funzionalità sul lato server che è necessario gestire e amministrare, che vengono descritte di seguito:  
  
-   Servizio Web ReportServer, eseguito con il servizio del server di report.  
  
-   Applicazioni di elaborazione in background che gestiscono operazioni pianificate e il recapito di report.  
  
-   Database del server di report.  
  
 Per amministrare interamente un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , è necessario disporre delle autorizzazioni seguenti:  
  
-   Appartenenza al gruppo Administrators locale nel computer server di report. Se l'installazione include funzionalità del server in esecuzione in computer remoti e se si desidera gestire i server tramite una connessione remota, è necessario disporre delle autorizzazioni di amministratore in tali computer.  
  
-   Autorizzazioni di amministratore del database per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita il database.  
  
-   Se si sta installando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in un controller di dominio, è necessario essere un amministratore di dominio.  
  
##  <a name="bkmk_managecontent"></a>Gestione del contenuto  
 Le operazioni di gestione del contenuto in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]includono la gestione dei report, dei modelli, delle cartelle, delle risorse e delle origini dati condivise. È possibile gestire questi elementi singolarmente tramite impostazioni di sicurezza e proprietà. Ogni elemento può essere spostato in una posizione diversa nello spazio dei nomi delle cartelle del server di report. Per gestire gli elementi in modo efficiente, è necessario conoscere quali attività vengono eseguite da un utente con ruolo Gestione contenuto.  
  
> [!NOTE]  
>  La gestione del contenuto è un'operazione diversa dall'amministrazione di un server di report. Per ulteriori informazioni sulla gestione dell'ambiente in cui viene eseguito un server di report, vedere [amministrazione (Reporting Services)](reporting-services-report-server-native-mode.md).  
  
 Nella gestione del contenuto sono incluse le attività seguenti:  
  
-   Sicurezza del sito e degli elementi del server di report mediante l'applicazione della sicurezza basata sui ruoli disponibile in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Gestione della struttura della gerarchia di cartelle del server di report mediante l'aggiunta, la modifica e l'eliminazione di cartelle.  
  
-   Impostazione di valori predefiniti e proprietà relativi a elementi gestiti dal server di report. È ad esempio possibile impostare valori massimi di riferimento che determinano i criteri di archiviazione della cronologia dei report.  
  
-   Creazione di origini dei dati condivise che è possibile utilizzare in sostituzione di connessioni a origini dei dati specifiche dei report. Un utente con ruolo Pubblicazione o Gestione contenuto può selezionare un'origine dei dati diversa da quella definita originariamente per un report, ad esempio per sostituire un riferimento a un database di prova con un riferimento a un database di produzione.  
  
-   Creazione di pianificazioni condivise che possono essere utilizzate in sostituzione di pianificazioni specifiche del report e della sottoscrizione, semplificando nel tempo la gestione delle informazioni sulla pianificazione.  
  
-   Creazione di sottoscrizioni guidate dai dati che generano elenchi di destinatari tramite il recupero di dati da un archivio dati.  
  
-   Bilanciamento delle richieste di elaborazione di report inviate al server tramite la pianificazione dell'elaborazione dei report stessi e l'indicazione di quali possono essere eseguiti su richiesta e quali vengono caricati dalla cache.  
  
 Le autorizzazioni per eseguire le attività di gestione vengono fornite in due ruoli predefiniti, ovvero **Amministratore sistema** e **Gestione contenuto**. Per gestire in modo efficiente contenuto di un server di report, è necessario che un utente sia assegnato a entrambi ruoli. Per altre informazioni su questi ruoli predefiniti, vedere [Ruoli e autorizzazioni &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md).  
  
 Gli strumenti per la gestione dei contenuti del server di report includono [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o Gestione report. 
  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] consente di impostare valori predefiniti e di abilitare funzionalità. Gestione report consente di concedere agli utenti l'accesso a elementi e operazioni del server di report, visualizzare e utilizzare report e altri tipi di contenuto, nonché visualizzare e utilizzare tutti gli elementi condivisi e le funzionalità di distribuzione del report.  
  
##  <a name="bkmk_manageresources"></a>Sicurezza e gestione di una risorsa  
 Una risorsa è un elemento gestito che viene archiviato, ma non elaborato, in un server di report. In genere, una risorsa fornisce contenuto esterno per gli utenti dei report. Ad esempio un'immagine in un file con estensione jpg o un file HTML che descrive le regole business utilizzate in un report. Il file in formato JPG o HTML viene archiviato nel server di report, che tuttavia lo invia direttamente al browser anziché prima elaborarlo.  
  
 Per aggiungere una risorsa a un server di report, caricare o pubblicare un file:  
  
|Operazione|Tipo file|  
|---------------|---------------|  
|Caricamento|Tutti i file vengono caricati come risorse ad eccezioni dei file di definizione del report (con estensione rdl) e del modello di report (con estensione smdl).<br /><br /> Per caricare una risorsa, utilizzare Gestione report se il server di report è in esecuzione in modalità nativa o una pagina di applicazione su un sito di SharePoint se il server è in esecuzione in modalità integrata SharePoint. Per altre informazioni, vedere [Caricare un file o un report &#40;Gestione report&#41;](../reports/upload-a-file-or-report-report-manager.md) o [Caricare documenti in una raccolta di SharePoint &#40;Reporting Services in modalità SharePoint&#41;](../upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md).|  
|Pubblica|Tutti i file in un progetto vengono caricati come risorse, ad eccezione dei file dell'origine dati con estensione rdl, smdl e rds. Per pubblicare una risorsa, aggiungere un elemento esistente a un progetto in Progettazione report, quindi pubblicare il progetto in un server di report.|  
  
 Tutte le risorse provengono da file presenti nel file system, caricati successivamente in un server di report. Ad eccezione dei limiti per le dimensioni del file predefinite di 4 MB imposte da ASP.NET, non sono presenti restrizioni sui tipi di file che è possibile caricare. Alcuni tipi di file risultano tuttavia più adatti di altri con tipo MIME equivalente per la pubblicazione in un server di report come risorse. Ad esempio, le risorse basate su file HTML e JPG vengono aperte in una finestra del browser quando l'utente fa clic sulla risorsa. In tal modo i file HTML vengono visualizzati come pagine Web e i file JPG come immagini visibili all'utente. Al contrario le risorse con tipi MIME non equivalenti, ad esempio file di applicazioni desktop, non vengono visualizzate in alcun modo nella finestra del browser.  
  
 Il fatto che una risorsa risulti visibile agli utenti di un report dipende dalle funzionalità del browser in uso. Poiché le risorse non vengono elaborate dal server di report, il browser deve fornire la funzionalità di visualizzazione per eseguire il rendering di un tipo MIME specifico. Se il browser non è in grado di eseguire il rendering del contenuto, gli utenti che visualizzeranno la risorsa ne vedranno esclusivamente le proprietà generali.  
  
 Le risorse sono presenti come elementi denominati nella gerarchia delle cartelle del server di report insieme ai report, alle origini dati condivise, alle pianificazioni condivise e alle cartelle. È possibile ricercare, visualizzare, proteggere impostare proprietà relative alle risorse analogamente a qualsiasi altro elemento presente in un server di report. Per visualizzare o gestire una risorsa, è necessario disporre delle attività Visualizzazione di risorse o Gestione di risorse nella propria assegnazione di ruolo.  
  
##  <a name="bkmk_referenceimage"></a>Riferimento a una risorsa immagine da un report  
 Le risorse possono contenere un'immagine cui si fa riferimento in un report. Se i requisiti del report includono l'utilizzo di immagini esterne, considerare i vantaggi seguenti relativi all'archiviazione di un'immagine come risorsa:  
  
-   Archiviazione centralizzata nel database del server di report. Se il database del server di report e il relativo contenuto vengono spostati in un altro computer, l'immagine esterna rimane con il report. Non è necessario tenere traccia di file di immagine archiviato su disco in computer diversi.  
  
-   sicurezza garantita dalle assegnazioni di ruolo anziché a livello di file system. Le stesse autorizzazioni utilizzate per visualizzare un report possono essere applicate alla risorsa. Al contrario, se si archivia l'immagine su disco, è necessario verificare che l'account utente anonimo o l'account di esecuzione automatica disponga delle autorizzazioni per accedere al file.  
  
 Per utilizzare una risorsa immagine in un report, aggiungere il file di immagine al progetto e pubblicarlo insieme al report. Dopo la pubblicazione, è possibile aggiornare il riferimento all'immagine nel report in modo che punti alla risorsa nel server di report e successivamente ripubblicare il report per salvare le modifiche. È possibile a questo punto aggiornare l'immagine in modo indipendente dal report ripubblicando la risorsa. Nel report viene utilizzata la versione più recente dell'immagine disponibile nel server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare e amministrare un server di report &#40;modalità nativa SSRS&#41;](configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Risoluzione dei problemi di installazione di Reporting Services](../install-windows/troubleshoot-a-reporting-services-installation.md)  
  
  
