---
title: Creare una sottoscrizione guidata dai dati (esercitazione su SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a6e1399c97e77a2b7b0bb68a8022effefb1d4814
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59964107"
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>Creare una sottoscrizione guidata dai dati (esercitazione su SSRS)
  In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono disponibili sottoscrizioni guidate dai dati che consentono di personalizzare la distribuzione di un report in base ai dati dinamici del Sottoscrittore. Le sottoscrizioni guidate dai dati sono progettate per i tipi di scenari seguenti:  
  
-   Per la distribuzione di report a un ampio pool di destinatari la cui appartenenza può cambiare in base alla distribuzione. Ad esempio, per la distribuzione di un report mensile a tutti i clienti attuali.  
  
-   Per la distribuzione di report a un gruppo specifico di destinatari in base a criteri predefiniti. Ad esempio, per l'invio di un report relativo ai dati delle vendite ai primi dieci responsabili delle vendite di un'organizzazione.  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 In questa esercitazione vengono descritte le procedure per l'utilizzo di sottoscrizioni guidate dai dati mediante un semplice esempio che ne illustra i concetti.  
  
 L'esercitazione è suddivisa in tre lezioni:  
  
 [Lezione 1: Creazione di un Database Sottoscrittore di esempio](lesson-1-creating-a-sample-subscriber-database.md)  
 In questa lezione verranno descritte le procedure per la creazione di un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] locale che contiene informazioni sui Sottoscrittori.  
  
 [Lezione 2: Modifica delle proprietà dell'origine dati del report](lesson-2-modifying-the-report-data-source-properties.md)  
 In questa lezione verranno descritte le procedure per la modifica delle proprietà dell'origine dati del report in modo che il report possa essere eseguito automaticamente. Le credenziali archiviate sono necessarie per l'elaborazione automatica. Inoltre, verrà modificato il set di dati del report per includere un parametro fornito dai dati del sottoscrittore.  
  
 [Lezione 3: Definizione di una sottoscrizione guidata dai dati](lesson-3-defining-a-data-driven-subscription.md)  
 In questa lezione verranno descritte le procedure per la definizione di una sottoscrizione guidata dai dati. In questa lezione viene introdotta la procedura guidata che consente di eseguire in modo semplificato i passaggi necessari per creare sottoscrizioni guidate dai dati.  
  
## <a name="requirements"></a>Requisiti  
 Le sottoscrizioni guidate dai dati vengono in genere create e gestite da amministratori di server di report. Per creare sottoscrizioni guidate dai dati è necessario conoscere le modalità di compilazione delle query e delle origini dei dati contenenti i dati del Sottoscrittore. È inoltre necessario disporre di autorizzazioni elevate per un server di report.  
  
 Nell'esercitazione verrà utilizzato il report creato nell'esercitazione [creare un Report tabella semplice &#40;esercitazione su SSRS&#41; ](create-a-basic-table-report-ssrs-tutorial.md) e i dati da [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]  
  
 Per utilizzare l'esercitazione è necessario che nel sistema siano installati i componenti seguenti:  
  
-   Un'edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che supporta sottoscrizioni guidate dai dati. Per altre informazioni, vedere [edizioni e componenti di SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md).  
  
-   Il server di report deve essere eseguito in modalità nativa. L'interfaccia utente descritta in questa esercitazione è basata su un server di report in modalità nativa. Le sottoscrizioni sono supportate in server di report in modalità SharePoint ma l'interfaccia utente sarà diversa da quella descritta in questa esercitazione.  
  
-   È necessario che il servizio SQL Server Agent sia in esecuzione.  
  
-   Un report con parametri. In questa esercitazione si presuppone l'uso del report di esempio `Sales Orders` creato durante l'esercitazione [Creare un report di tabelle semplice &#40;Esercitazione su SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md).  
  
-   Il database di esempio [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] che contiene i dati per il report di esempio.  
  
-   Un'assegnazione di ruolo che include l'attività Gestione di tutte le sottoscrizioni nel report di esempio. Questa attività è necessaria per la definizione di una sottoscrizione guidata dai dati. Per gli amministratori del computer, l'assegnazione di ruolo predefinita per gli amministratori locali fornisce le autorizzazioni necessarie per la creazione di sottoscrizioni guidate dai dati. Per altre informazioni, vedere [Concessione di autorizzazioni in un server di report in modalità nativa](security/granting-permissions-on-a-native-mode-report-server.md).  
  
-   Una cartella condivisa per la quale si dispone di autorizzazioni di scrittura. La cartella condivisa deve essere accessibile su una connessione di rete.  
  
 **Tempo previsto per il completamento dell'esercitazione:** 30 minuti. Ulteriori 30 minuti qualora l'esercitazione sul report di base non venga completata.  
  
## <a name="see-also"></a>Vedere anche  
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [Creare un report tabella semplice &#40;esercitazione su SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
