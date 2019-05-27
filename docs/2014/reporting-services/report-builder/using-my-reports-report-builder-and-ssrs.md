---
title: Using My Reports (Report Builder and SSRS) (Uso di Report personali (Generatore report e SSRS)) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 49c3c1da-b106-41f6-9173-16ff225bade8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 410cb4de6b89052493618404df3e595fd6999936
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107583"
---
# <a name="using-my-reports-report-builder-and-ssrs"></a>Utilizzo della cartella Report personali (Generatore report e SSRS)
  In un server di report configurato in modalità nativa, la cartella Report personali è un'area di lavoro personale che è possibile utilizzare per archiviare e gestire i report di cui si è proprietari. Le altre cartelle del server di report sono pubbliche e in genere è necessario disporre di autorizzazioni avanzate per aggiungere o modificare contenuto in tali cartelle. Al contrario, la cartella Report personali è un'area di lavoro gestita dall'utente nella quale è possibile aggiungere o rimuovere report o cartelle e salvare report collegati con impostazioni personalizzate.  
  
 Concettualmente, la cartella Report personali è simile alla cartella Documenti del file system di Windows. Nonostante ogni utente sia proprietario di una cartella Report personali, la cartella di ciascuno è diversa da quelle di tutti gli altri utenti. L'accesso alla cartella Report personali di un determinato utente è consentito solo all'utente stesso e agli amministratori del server di report.  
  
 La caratteristica funzionalità Report personali è facoltativa e può essere disabilitata da un amministratore del server di report. Se è abilitata, viene visualizzata una cartella Report personali nella cartella Home, alla quale è possibile accedere tramite Gestione report o un Web browser. Per altre informazioni, vedere [Ricerca e visualizzazione di report in Gestione report &#40;Generatore report e SSRS&#41;](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md).  
  
 In un server di report configurato nella modalità integrata SharePoint, non esiste una cartella Report personali equivalente. Per altre informazioni, vedere [Ricerca, visualizzazione e gestione dei report &#40;Generatore report SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="ways-to-use-my-reports"></a>Modalità di utilizzo della funzionalità Report personali  
 Quando viene creata, la cartella Report personali è vuota. In seguito, è possibile aggiungervi report, cartelle e altri elementi. Di seguito vengono indicate alcune delle possibili modalità di aggiunta di contenuto alla cartella Report personali.  
  
-   Creare un report collegato personale e archiviarlo nella cartella Report personali. Non tutti i report possono essere collegati. Per altre informazioni, vedere [Creare un report collegato](../reports/create-a-linked-report.md).  
  
-   Caricare un file di definizione del report (estensione rdl), un file di modello del report (estensione smdl) o altri file dal file system. È possibile caricare qualsiasi tipo di file, che verranno tuttavia elaborati dal server di report solo i file di report dispongono dell'estensione rdl o smdl. Per altre informazioni, vedere "Definizioni dei report" nella [documentazione relativa a Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) inclusa nella documentazione online SQL Server e [Caricare un file o un report &#40;Gestione report&#41;](../reports/upload-a-file-or-report-report-manager.md).  
  
-   Creare e pubblicare i report personali nella cartella Report personali. Per altre informazioni, vedere [Visualizzazione di progettazione report &#40;Generatore report&#41;](report-design-view-report-builder.md).  
  
 Le autorizzazioni per la cartella Report personali, in genere, consentono al proprietario di gestire la cartella stessa. Tuttavia, è l'amministratore del server di report che decide quali attività possono essere eseguite dagli utenti. Se non si dispone di autorizzazioni sufficienti per utilizzare la cartella Report personali, rivolgersi all'amministratore del server di report.  
  
## <a name="searching-my-reports"></a>Ricerche nella cartella Report personali  
 Quando un utente esegue una ricerca in un database del server di report, tra i contenuti in cui viene eseguita la ricerca vengono inclusi quelli della cartella Report personali dell'utente mentre sono esclusi quelli delle cartelle Report personali degli altri utenti. Nell'elenco dei risultati della ricerca vengono inclusi solo i report a cui l'utente che ha eseguito la ricerca è autorizzato ad accedere.  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
