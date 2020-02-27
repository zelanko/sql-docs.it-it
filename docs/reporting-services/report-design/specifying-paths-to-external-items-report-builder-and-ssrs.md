---
title: Specifica di percorsi di elementi esterni (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4fe513da-f3c5-479c-9fec-8662b91a0d6d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cad68b0b99479b074e04760f419e12ec9837aac3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77080914"
---
# <a name="specifying-paths-to-external-items-report-builder-and-ssrs"></a>Specifica di percorsi di elementi esterni (Generatore report e SSRS)
  Nelle proprietà degli elementi del report è possibile specificare percorsi che facciano riferimento a elementi esterni al file di definizione del report archiviati in un server di report, ad esempio report drill-through, sottoreport e file di immagini.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
> [!NOTE]  
>  In Generatore report i percorsi degli elementi devono specificare elementi presenti in un server di report. I percorsi degli elementi di un file system non sono supportati. È possibile visualizzare in anteprima un report che utilizza questi elementi solo se si è connessi al server di report in cui si trovano gli elementi.  
  
 Quando si specifica un percorso di un elemento esterno in una finestra di dialogo relativa ad azioni, sottoreport o immagini, è possibile passare direttamente al server di report e selezionare l'elemento. Per specificare un report drill-through o un sottoreport è consigliabile individuare e selezionare l'elemento direttamente dal server di report. In questo modo, quando si specificano i parametri del report o del sottoreport, i nomi di parametro corretti risulteranno disponibili in un elenco a discesa. Se si modifica il percorso di un elemento in modo che punti a un altro elemento, è necessario aggiornare manualmente i valori e i nomi dei parametri nel modo appropriato.  
  
 In un server di report configurato in modalità nativa, specificare un nome di report drill-through senza l'estensione di file rdl.  
  
 In un server di report configurato in modalità integrata SharePoint, è necessario includere l'estensione di file rdl. Il percorso può essere uno dei seguenti:  
  
-   **Un percorso relativo dell'elemento del report principale,** ad esempio ../TuttiSottoreport/Sottoreport1. In questo esempio i puntini di sospensione **..** indicano la cartella di livello superiore rispetto a quella in cui si trova il report principale.  
  
    > [!NOTE]  
    >  Quando il report viene eseguito in Generatore report, i percorsi relativi non sono supportati. Per visualizzare un report che utilizza percorsi relativi di elementi esterni, salvare il report nel server di report ed eseguirlo da tale server.  
  
-   **Un percorso completo dell'elemento.**  
  
    -   **Nel server di report:** Un percorso completo inizia da **/** la cartella Home, ad esempio /Report/TuttiSottoreport/Sottoreport1.  
  
    -   **In un sito di SharePoint** È necessario specificare il nome del report in un'espressione, includendo l'URL completo dell'elemento e l'estensione di file rdl, Ad esempio: `="https://server/site/library/folder/Report1.rdl"`.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere un'immagine esterna &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [Aggiungere un sottoreport e parametri &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [Aggiungere un'azione drill-through a un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  
