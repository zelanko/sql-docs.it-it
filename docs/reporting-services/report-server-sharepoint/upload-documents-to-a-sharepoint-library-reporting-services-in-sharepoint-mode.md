---
title: Caricare documenti in una raccolta di SharePoint (Reporting Services in modalità SharePoint) | Microsoft Docs
description: In SQL Server Reporting Services, in modalità SharePoint, è possibile caricare definizioni e modelli di report in una raccolta SharePoint.
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016'
ms.openlocfilehash: 0d033bdfe9ae0d2773e7c3d8622b7321ed60e02e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461422"
---
# <a name="upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode"></a>Caricare documenti in una raccolta di SharePoint (Reporting Services in modalità SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Definizioni e modelli di report possono essere caricati in una raccolta di SharePoint. Quando si carica un elemento del server di report, è necessario selezionare una raccolta o una cartella all'interno di una raccolta. Gli elementi del server di report non possono infatti essere caricati in un elenco o in una pagina.  

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

 Non è possibile caricare un file dell'origine dati (con estensione rds). Tali file tuttavia possono essere pubblicati da uno strumento di progettazione, ad esempio Progettazione report, in una raccolta di SharePoint. Durante la pubblicazione viene creato un nuovo file con estensione rsds utilizzando il file rds originale della soluzione. È inoltre possibile creare un nuovo file con estensione rsds in una raccolta di SharePoint, quindi impostare le proprietà di connessione all'origine dati nei report e nei modelli caricati in modo che venga utilizzata la nuova connessione.  
  
> [!NOTE]  
>  Il server di report deve essere configurato per la modalità SharePoint e l'istanza del prodotto SharePoint deve disporre del componente aggiuntivo Reporting Services, che fornisce file di programma per l'archiviazione di elementi del server di report, nonché l'accesso a questi elementi da un sito di SharePoint.  
  
 Per caricare un documento in una raccolta, è necessario disporre dell'autorizzazione "Aggiunta elementi" a livello del sito. Se si usano le impostazioni di sicurezza predefinite, questa autorizzazione viene concessa ai membri del gruppo **Proprietari** che dispongono del livello di autorizzazione Controllo completo e del gruppo **Membri** che dispongono del livello di autorizzazione Collaborazione.  
  
## <a name="add-a-report-definition-or-report-model-to-a-library"></a>Aggiungere la definizione o il modello di un report a una raccolta
  
1.  Aprire la raccolta o una cartella all'interno della raccolta. Se la raccolta non è aperta, fare clic sul nome della raccolta sulla barra di avvio veloce. Se il nome della raccolta non è visualizzato, fare clic su **Visualizza tutto il contenuto del sito** e quindi sul nome della raccolta desiderata.  
  
2.  Scegliere **Carica documento** dal menu **Carica**.  
  
3.  Per caricare un singolo file di un report o di un modello di report, selezionare un file di definizione di report (con estensione rdl) o di modello di report (con estensione smdl) e quindi fare clic su **OK**.  
  
     Se la definizione di report utilizza un file di origine dei dati condivisa (con estensione rsds) per archiviare le informazioni di connessione in un'origine dati esterna, i file con estensione rdl e rsds possono essere caricati contemporaneamente. A tale scopo, fare clic su **Carica più documenti**, specificare entrambi i file e quindi fare clic su **OK**.  
  
 Se si carica un report che contiene riferimenti a origini dei dati condivise, modelli di report o sottoreport, tali riferimenti verranno interrotti nel report al momento del caricamento dei file. Per altre informazioni su come reimpostare i riferimenti, vedere [Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](/previous-versions/sql/).  
  
 Quando si apre un report dopo averlo caricato, tale report viene eseguito su richiesta recuperando dati in tempo reale dall'origine dei dati. È possibile configurare il report per il recupero dei dati in una pianificazione o l'utilizzo di dati memorizzati nella cache. Per altre informazioni, vedere [Impostare le opzioni di elaborazione &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md).  
  
 Un report può contenere parametri che consentono agli utenti di filtrare i dati. È possibile configurare i parametri in modo che utilizzino valori specifici o modificare la visualizzazione di tali parametri per gli utenti. Per altre informazioni, vedere [Impostare i parametri per un report pubblicato &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Vedere anche

 [Pubblicare un report in una raccolta di SharePoint](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Pubblicare un'origine dati condivisa in una raccolta di SharePoint](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)