---
title: Stampare report (SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 4bad1b6e-7d94-4b17-9502-ccd3dce0fdd9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 45b38940afcd0fe73ad2c79abc59db9dc7b549b3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581161"
---
# <a name="print-reports---reporting-services-ssrs"></a>Stampare report - Reporting Services (SSRS)
  Dopo avere salvato un report in un server di report, è possibile visualizzarlo e stamparlo dal portale Web o da qualsiasi applicazione usata per visualizzare un report esportato. Prima di salvare un report, è possibile stamparlo durante l'anteprima.  
  
 Tutte le operazioni di elaborazione della stampa vengono eseguite su richiesta e nel computer client. Non è disponibile una funzionalità di stampa sul lato server che consente di eseguire il routing di un processo di stampa direttamente da un server di report a una stampante collegata al server Web. Le stampanti e le opzioni di stampa vengono selezionate da utenti singoli del report tramite una finestra di dialogo **Stampa** standard.  
  
 Gli autori che progettano report specifici per l'output su stampante possono utilizzare interruzioni di pagina, intestazioni e piè di pagina, espressioni e immagini di sfondo per creare una struttura adatta per la stampa. Gli elementi di progettazione di report specifici per l'output di stampa includono i termini e le condizioni stampati sul retro di ogni report oppure gli elementi grafici e di testo che riproducono la carta intestata.  
  
 Poiché l'impaginazione è diversa per formati di rendering differenti, è possibile che non si riesca a ottenere un output di stampa ottimale per ogni report in tutti i formati di rendering. Di seguito sono elencati alcuni esempi:  
  
1.  Le pagine dei report sono progettate per contenere quantità variabili di dati. I report che includono una matrice, ad esempio, possono utilizzare una pagina per estendere le dimensioni in senso orizzontale e verticale a seconda che l'utente attivi o disattivi in modo dinamico righe e colonne. L'utente che non espande una matrice ottiene risultati di stampa diversi rispetto all'utente che la espande.  
  
2.  Non è possibile combinare pagine con orientamento verticale e orizzontale nello stesso report, né creare un layout per la stampa sostitutivo o parallelo al layout di un report visualizzato in un browser o in un'altra applicazione.  
  
3.  Per la maggior parte dei report esportati, la stampa include tutti gli elementi visibili, esattamente come sono visualizzati sullo schermo. Lo spazio vuoto nell'area di progettazione del report viene conservato. Per aggiungere o rimuovere le pagine vuote aggiuntive orizzontalmente, impostare la larghezza della pagina del report.  
  
> [!NOTE]  
>  Le stampe di report HTML possono contenere solo il contenuto della prima pagina, se si utilizza il comando Stampa del browser. Per ottenere risultati migliori, stampare i report HTML con la funzionalità di stampa su client di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [Stampare i report da un browser con il controllo di stampa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Stampare i report da un browser con il controllo di stampa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)  
 Descrive come usare la funzionalità di stampa lato client per stampare report dal portale Web.  
  
 [Stampare i report da altre applicazioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/print-reports-from-other-applications-report-builder-and-ssrs.md)  
 Descrive come stampare report esportati in un'altra applicazione.  
  
 [Stampare un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
 Vengono fornite istruzioni dettagliate su come stampare un report, come controllare i margini di una pagina e come specificare il formato carta per i report di cui verrà eseguito il rendering da renderer di interruzioni di pagina manuali, ovvero PDF, immagine o stampa.  
  
## <a name="see-also"></a>Vedere anche  
 [Esportare report &#40;Generatore Report e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Intestazioni di pagina e piè di pagina &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Immagini &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)  
  
  
