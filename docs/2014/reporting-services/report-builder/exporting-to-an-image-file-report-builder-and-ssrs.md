---
title: Esportazione in un file di immagine (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fd3a6e7126775479ae7ca0c6b6d138a0625476af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107885"
---
# <a name="exporting-to-an-image-file-report-builder-and-ssrs"></a>Esportazione in un file di immagine (Generatore report e SSRS)
  L'estensione per il rendering delle immagini genera bitmap o metafile dei report. Per impostazione predefinita, l'estensione per il rendering delle immagini crea un file TIFF del report, che può essere visualizzato in più pagine. Nel client l'immagine può essere visualizzata in un visualizzatore di immagini e stampata. In questo argomento vengono fornite informazioni specifiche sul renderer di immagini e vengono descritte le eccezioni alle regole di rendering.  
  
 L'estensione per il rendering delle immagini consente di generare file in tutti i formati supportati da [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG e TIFF. Per il formato TIFF, il nome file del flusso primario è *NomeReport*.tif. Per tutti gli altri formati, di cui viene eseguito il rendering come singola pagina per file, il nome file è *ReportName_Page.ext* , dove *ext* è l'estensione di file per il formato scelto. Per produrre un file in un altro formato di immagine supportato, specificare una delle stringhe elencate in precedenza nell'impostazione **OutputFormatDeviceInfo** .  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="supported-image-formats"></a><a name="SupportedImageFormats"></a> Formati di immagine supportati  
 Nella tabella seguente sono illustrati l'estensione di file e il tipo MIME per ogni formato del renderer di immagini.  
  
|**Type**|**Estensione**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|BMP|image/bmp|  
|GIF|GIF|image/gif|  
|JPEG|JPEG|image/jpeg|  
|PNG|png|image/png|  
|TIFF|tif|image/tiff|  
|EMF|EMF|image/emf|  
|EMFPlus|EMF|image/emf|  
  
  
##  <a name="rendering-multiple-pages"></a><a name="RenderingMultiplePages"></a> Rendering di più pagine  
 L'unico formato che supporta documenti a più pagine in un unico file è TIFF. Altri formati, ad esempio JPG o PNG, generano una pagina alla volta e richiedono una chiamata distinta all'estensione per il rendering per ogni pagina.  
  
  
##  <a name="interactivity"></a><a name="Interactivity"></a> Interattività  
 L'interattività non è supportata in alcun formato di immagine generato da questo renderer. Non viene eseguito il rendering dei seguenti elementi interattivi:  
  
-   Collegamenti ipertestuali  
  
-   Elementi visualizzati o nascosti  
  
-   Mappa documento  
  
-   Collegamenti drill-through o click-through  
  
-   Ordinamento dell'utente finale  
  
-   Intestazioni fisse  
  
-   Segnalibri  
  
  
##  <a name="device-information-settings"></a><a name="DeviceInfo"></a>Impostazioni relative alle informazioni sul dispositivo  
 È possibile modificare alcune impostazioni predefinite per questo renderer modificando le impostazioni relative alle informazioni sul dispositivo. Per ulteriori informazioni, vedere [Image Device Information Settings](../image-device-information-settings.md).  
  
  
## <a name="see-also"></a>Vedi anche  
 [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamenti di rendering &#40;Generatore report e SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funzionalità interattiva per estensioni per il rendering di report diverse &#40;Generatore report e SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Rendering degli elementi del report &#40;Generatore report e SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
