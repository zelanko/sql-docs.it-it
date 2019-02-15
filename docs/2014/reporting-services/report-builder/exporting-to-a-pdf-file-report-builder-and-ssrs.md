---
title: Esportazione in un file PDF (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f22497b7-f6c1-4c7b-b831-8c731e26ae37
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a52a828227c316c37e90f6d2ecc95b3bce85747d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295219"
---
# <a name="exporting-to-a-pdf-file-report-builder-and-ssrs"></a>Esportazione in un file PDF (Generatore report e SSRS)
  L'estensione per il rendering PDF consente di eseguire il rendering di un report in file che possono essere aperti in Adobe Acrobat e in altri visualizzatori PDF di terze parti che supportano il formato PDF 1.3. Anche se PDF 1.3 è compatibile con Adobe Acrobat 4.0 e versioni successive, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta Adobe Acrobat 6 e versioni successive. Non è necessaria l'applicazione Adobe per convertire i report mediante l'estensione per il rendering. Per visualizzare o stampare i report in formato PDF è tuttavia necessario disporre di visualizzatori PDF, ad esempio Adobe Acrobat.  
  
 L'estensione per il rendering PDF supporta i caratteri ANSI ed è in grado di convertire i caratteri Unicode dalle lingue giapponese, coreana, cinese tradizionale, cinese semplificato, cirillico, ebraico e arabo con alcune limitazioni. Per altre informazioni sulle limitazioni, vedere [esportazione di report &#40;Generatore Report e SSRS&#41;](export-reports-report-builder-and-ssrs.md).  
  
 Il renderer PDF è un renderer di pagine fisiche e, pertanto, presenta un comportamento di paginazione diverso da quello di altri renderer, ad esempio HTML e Excel. In questo argomento vengono fornite informazioni specifiche sul renderer PDF e vengono descritte le eccezioni alle regole.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="FontRequirements"></a> Incorporamento dei tipi di carattere  
 Se possibile, l'estensione per il rendering in PDF incorpora il subset di ogni tipo di carattere necessario per la visualizzazione del report nel file PDF. I tipi di carattere usati nel report devono essere installati nel server di report. Quando il server di report genera un report in formato PDF, vengono usate le informazioni archiviate nel tipo di carattere a cui fa riferimento il report per creare i mapping dei caratteri nel file PDF. Se il tipo di carattere a cui viene fatto riferimento non è installato nel server di report, il file PDF risultante potrebbe non contenere i mapping appropriati e non essere visualizzato correttamente.  
  
 I tipi di carattere vengono incorporati nel file PDF quando si verificano le condizioni seguenti:  
  
-   L'autore del tipo di carattere concede privilegi per l'incorporamento dei tipi di carattere. I tipi di carattere installati includono una proprietà che indica se l'autore di tali caratteri desidera consentirne l'incorporamento in un documento. Se il valore della proprietà è EMBED_NOEMBEDDING, il tipo di carattere non viene incorporato nel file PDF. Per altre informazioni, vedere "TTGetEmbeddingType" nel sito msdn.microsoft.com.  
  
-   Il tipo di carattere è TrueType.  
  
-   Ai tipi di carattere viene fatto riferimento mediante elementi visibili in un report. Se un elemento fa riferimento a un tipo di carattere con la proprietà Hidden impostata su True, il tipo di carattere non è necessario per la visualizzazione dei dati sottoposti a rendering e non verrà incluso nel file. I tipi di carattere vengono incorporati solo quando sono necessari per la visualizzazione dei dati del report sottoposti a rendering.  
  
 Se per un tipo di carattere vengono soddisfatte tutte queste condizioni, tale tipo di carattere viene incorporato nel file PDF. Se non vengono soddisfatte una o più di queste condizioni, il tipo di carattere non viene incorporato nel file PDF.  
  
> [!NOTE]  
>  Sebbene le condizioni vengano soddisfatte, esiste una circostanza in cui i caratteri non sono incorporati nel file PDF. Se i tipi di carattere usati sono quelli nella specifica PDF noti in genere come caratteri standard di tipo 1 o caratteri di base quattordici, i caratteri non sono incorporati per il contenuto ANSI.  
  
  
  
### <a name="fonts-on-the-client-computer"></a>Tipi di carattere nel computer client  
 Quando un tipo di carattere viene incorporato nel file PDF, non è necessario che sia installato nel computer usato per visualizzare il report, ovvero il computer client, per garantire una corretta visualizzazione del report.  
  
 Quando un tipo di carattere non viene incorporato nel file PDF, è necessario che nel computer client sia installato il tipo di carattere appropriato per garantire una corretta visualizzazione del report. Se il tipo di carattere non è installato nel computer client, nel file PDF viene visualizzato un punto interrogativo (?) in corrispondenza dei caratteri non supportati.  
  
### <a name="verifying-fonts-in-a-pdf-file"></a>Verifica dei tipi di carattere in un file PDF  
 Le differenze nell'output PDF si verificano più spesso quando si utilizza un tipo di carattere che non supporta caratteri non latini in un report nel quale vengono successivamente aggiunti caratteri non latini. Per assicurarsi che il rendering del report venga eseguito correttamente, è consigliabile verificare l'output del rendering in formato PDF sia nel server di report che nei computer client.  
  
 A tale scopo, la visualizzazione dell'anteprima del report o l'esportazione in HTML non risultano affidabili poiché il report verrà visualizzato in modo corretto grazie alla sostituzione automatica dei tipi di caratteri eseguita rispettivamente dall'interfaccia di progettazione grafica o da Microsoft Internet Explorer. Se nel server non sono disponibili glifi Unicode, è possibile che i caratteri vengano sostituiti da un punto interrogativo (?). Se nel client non è disponibile un determinato tipo di carattere, è possibile che i caratteri vengano sostituiti da riquadri (□).  
  
 I tipi di carattere incorporati nel file PDF sono inclusi come metadati nella proprietà Fonts salvata con il file.  
  
##  <a name="Metadata"></a> Metadati  
 Oltre al layout del report, l'estensione per il rendering in PDF scrive i metadati seguenti nel dizionario di informazioni del documento PDF.  
  
|Proprietà PDF|Creata da|  
|------------------|------------------|  
|`Title`|Attributo `Name` dell'elemento RDL `Report`.|  
|`Author`|Elemento RDL `Author`.|  
|`Subject`|Elemento RDL `Description`.|  
|`Creator`|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|`Producer`|Nome e versione dell'estensione per il rendering.|  
|`CreationDate`|Data e ora di esecuzione del report nel formato PDF `datetime`.|  
  
  
  
##  <a name="Interactivity"></a> Interattività  
 In PDF sono supportati alcuni elementi interattivi. Di seguito è riportata una descrizione di comportamenti specifici.  
  
### <a name="show-and-hide"></a>Elementi visualizzati e nascosti  
 Gli elementi con attivazione e disattivazione dinamica della visualizzazione non sono supportati in PDF. Il rendering del documento PDF viene eseguito in base allo stato corrente degli elementi del report. Ad esempio, se l'elemento è visualizzato la prima volta che il report viene eseguito, il rendering di tale elemento verrà eseguito. Il rendering delle immagini che è possibile visualizzare e nascondere non viene eseguito, se tali immagini sono nascoste quando il report viene esportato.  
  
### <a name="document-map"></a>Mappa documento  
 Se il report contiene etichette della mappa documento, al file PDF viene aggiunta una struttura del documento. Ogni etichetta della mappa documento viene visualizzata come voce nella struttura del documento nell'ordine in cui appare nel report. In Acrobat viene aggiunto un segnalibro di destinazione alla struttura del documento solo se viene eseguito il rendering della pagina in cui è presente.  
  
 Se viene eseguito il rendering di una singola pagina, non viene aggiunta alcuna struttura del documento. La mappa documento viene disposta gerarchicamente per riflettere il livello di nidificazione del report. La struttura del documento è accessibile in Acrobat nella scheda Segnalibri. Se si fa clic su una voce all'interno della struttura del documento, nel documento si passa alla posizione contrassegnata con il segnalibro.  
  
### <a name="bookmarks"></a>Segnalibri  
 I segnalibri non sono supportati nel rendering in PDF.  
  
### <a name="drillthrough-links"></a>Collegamenti drill-through  
 I collegamenti drill-through non sono supportati nel rendering in PDF. Il rendering dei collegamenti drill-through non viene eseguito come collegamenti su cui è possibile fare clic e non è possibile connettere i report drill-through alla destinazione del drill-through.  
  
### <a name="hyperlinks"></a>Collegamenti ipertestuali  
 Il rendering dei collegamenti ipertestuali dei report viene eseguito come collegamenti su cui è possibile fare clic nel file PDF. Quando si fa clic, da Acrobat verrà aperto il browser client predefinito in corrispondenza dell'URL del collegamento ipertestuale.  
  
  
  
##  <a name="Compression"></a> Compressione  
 La compressione dell'immagine è basata sul tipo di file originale dell'immagine. L'estensione per il rendering in PDF comprime i file PDF per impostazione predefinita.  
  
 Per mantenere la compressione per le immagini incluse nel file PDF, quando possibile, le immagini JPEG vengono archiviate in formato JPEG e tutti gli altri tipi di immagine in formato BMP.  
  
> [!NOTE]  
>  I file PDF non supportano l'incorporamento di immagini PNG.  
  
  
  
##  <a name="DeviceInfo"></a> Impostazioni relative alle informazioni sul dispositivo  
 È possibile modificare alcune impostazioni predefinite per questo renderer modificando le impostazioni relative alle informazioni sul dispositivo. Per altre informazioni, vedere [PDF Device Information Settings](../pdf-device-information-settings.md).  
  
  
  
## <a name="see-also"></a>Vedere anche  
 [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Tipi di rendering &#40;Generatore report e SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funzionalità interattiva per estensioni per il rendering di report differenti &#40;Generatore report e SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Rendering degli elementi del report &#40;Generatore report e SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
