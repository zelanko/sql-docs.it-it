---
title: Caricare file in una cartella | Microsoft Docs
ms.date: 06/17/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
- files [Reporting Services]
- folders [Reporting Services], uploading files to
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d93840b2b1b7354238ccae12ba3a540889038fb2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67228680"
---
# <a name="upload-files-to-a-folder"></a>Caricare file in una cartella
  È possibile caricare file dal file system e archiviarli come elementi gestiti in un database del server di report. La funzionalità di un file caricato dipende dal tipo di file.  
  
-   Il caricamento di un file con estensione rdl equivale alla pubblicazione di un report.  
  
-   Qualsiasi altro tipo di file caricato viene aggiunto al database del server di report come singolo oggetto binario. I file vengono pubblicati in un server di report come risorse e possono essere file di qualsiasi tipo. Se l'estensione del file corrisponde a un tipo MIME noto, viene utilizzata un'icona specifica per identificare il tipo di risorsa. In caso contrario, la risorsa viene indicata da un'icona di file generico.  
  
    >[!NOTE]  
    >Non è possibile caricare un file di origine dei dati del report con estensione rds per creare un'origine dei dati condivisa. Un file con estensione rds viene utilizzato solo in Progettazione report. Tale file non fornisce il contenuto per un elemento dell'origine dati condivisa definito e gestito tramite il portale Web. In alternativa al caricamento è possibile creare uno script per la creazione di un'origine dei dati condivisa in base a un file con estensione rds.  
  
 Le dimensioni massime del file per gli elementi caricati sono pari a 2 GB e possono essere impostate usando la proprietà MaxFileSizeMb in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 I file caricati in un database del server di report sono visualizzati nella gerarchia di cartelle con le icone seguenti.  
  
  ![Icone di file caricabili del server di report](../../reporting-services/report-server/media/upload-files-to-a-folder/report-server-uploadable-file-icons.png)
  
 I file caricati vengono inseriti automaticamente nella cartella selezionata. È pertanto possibile passare alla cartella desiderata prima di caricare il file oppure spostare il file nella cartella desiderata dopo averlo caricato.  
  
 Per caricare un file, usare il portale Web. La possibilità o meno di caricare file in un server di report dipende dalle attività incluse nell'assegnazione di ruolo. Se vengono utilizzate le impostazioni di sicurezza predefinite, gli amministratori locali possono aggiungere elementi a un server di report. Se è attivata la funzionalità Report personali, qualsiasi utente con una cartella Report personali disporrà dell'autorizzazione per caricare elementi in quella cartella. Se si utilizzano assegnazioni di ruolo personalizzate, tali assegnazioni devono includere attività che supportano la gestione delle cartelle.  
  
|Per|Includere queste attività|  
|----------------|-------------------------|  
|Caricamento di un file con estensione rdl in una cartella|Gestione di report|  
|Caricamento di qualsiasi file come oggetto binario|Gestione di risorse|  
|Visualizzazione del contenuto di una cartella|Visualizzazione di risorse, Visualizzazione di report|  
  
## <a name="see-also"></a>Vedere anche  
 [Portale Web di un server di report (modalità nativa SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)  
 [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Attività e autorizzazioni](../../reporting-services/security/tasks-and-permissions.md)   
 [Caricare un file o un report nel server di report](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)   
  