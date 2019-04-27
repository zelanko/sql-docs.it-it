---
title: Pagina Visualizza, report (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4874ba29-429b-4dd4-a8cb-d4f087237dc2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d36a9e8b5e4b46283b78f07c27834a79993faeab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62647675"
---
# <a name="view-page-reports-report-manager"></a>Pagina Visualizza, Report (Gestione report)
  La pagina Visualizza per i report consente di visualizzare un report. La prima volta che si apre un report in Gestione report, questo viene visualizzato in formato HTML. I report HTML includono una barra degli strumenti dei report visualizzata nella parte superiore del report, che consente di spostarsi tra le pagine del report, eseguire ricerche all'interno di un report oppure esportarlo in un diverso formato. Nella figura seguente viene illustrata la barra degli strumenti dei report.  
  
 ![Barra degli strumenti dei report](media/htmlviewer-toolbar.gif "Barra degli strumenti dei report")  
Barra degli strumenti dei report  
  
 In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]è possibile configurare i report per l'esecuzione su richiesta o da uno snapshot dell'esecuzione del report. Se un report viene eseguito su richiesta, tutte le operazioni di elaborazione dei dati e del report vengono eseguite ogni volta che il report viene aperto. Se si visualizza un report configurato per l'esecuzione come snapshot dell'esecuzione del report, l'elaborazione dei dati avviene alla creazione del report.  
  
## <a name="exporting-reports"></a>Esportazione di report  
 Non tutte le caratteristiche dei report sono disponibili in tutti i formati di esportazione. Se si esporta un report HTML in un altro formato, ci saranno alcune differenze nell'aspetto del report. Inoltre, se il report include caratteristiche interattive quali collegamenti ipertestuali, segnalibri e mappe documenti, tali caratteristiche potrebbero non essere disponibili oppure non funzionare allo stesso modo nel nuovo formato.  
  
## <a name="generating-data-feeds-from-report-data"></a>Generazione di feed di dati dai dati del report  
 È possibile generare feed di dati dai report. L'estensione per il rendering Atom di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] genera due documenti conformi a Atom: un documento di servizio Atom che elenca i feed di dati forniti report e i feed di dati contenuti nei dati del report. I feed dei dati vengono generati da [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in un formato conforme a Atom 1.0 standardizzato che è leggibile e interscambiabile con applicazioni che utilizzano feed di dati conformi a Atom. Ad esempio il client [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] può utilizzare feed di dati generati dai report.  
  
## <a name="running-parameterized-reports"></a>Esecuzione di report con parametri  
 Un report in cui sono disponibili campi di input e il pulsante **Visualizza report** è un report con parametri. Per visualizzare un report con parametri potrebbe essere necessario specificare i valori da utilizzare per l'esecuzione del report.  
  
> [!NOTE]  
>  Gli snapshot dell'esecuzione del report e alcuni formati di esportazione non sono disponibili in tutte le edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
