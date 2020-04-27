---
title: Finestra di dialogo Proprietà immagine, generale (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10051"
- sql12.rtp.rptdesigner.pictureproperties.general.f1
ms.assetid: c2218b93-f7fe-46ef-995f-d7dadf9752ec
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8a66c424bfe5bd4a2587140a0f5238f46833a061
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109024"
---
# <a name="image-properties-dialog-box-general-report-builder-and-ssrs"></a>Finestra di dialogo Proprietà immagine, Generale (Generatore report e SSRS)
  Selezionare **Generale** nella finestra di dialogo **Proprietà immagine** per aggiungere un'immagine, modificare il nome predefinito dell'immagine e aggiungere il testo della descrizione comando.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Digitare un nome per l'elemento. Il nome deve essere univoco nel report. Per impostazione predefinita, viene assegnato un nome generale, ad esempio Immagine1 o Immagine2.  
  
 **Descrizione comando**  
 Digitare un testo o un'espressione che restituisca una descrizione comando. Fare clic sul pulsante espressione (*FX*) per modificare l'espressione. La descrizione comando viene visualizzata quando l'utente posiziona il puntatore del mouse sull'elemento in un report HTML. ****  
  
 **Selezionare l'origine dell'immagine**  
 Indicare il percorso di archiviazione dell'immagine in modo da specificare da dove il componente Elaborazione report recupererà l'immagine durante il rendering del report.  
  
-   **Esterna** Scegliere questa opzione se si desidera che l'immagine continui ad essere disponibile come file su un server di report o un server Web.  
  
-   **Incorporata** Scegliere questa opzione se si desidera incorporare l'immagine nel report.  
  
-   **Database** Scegliere questa opzione se si desidera includere un nome di campo del database che rappresenti le immagini da includere nel report.  
  
 **Utilizzare questa immagine**  
 Questa opzione viene visualizzata quando si seleziona l'opzione **Incorporata** o **Esterna** .  
  
 Se si intende incorporare l'immagine, selezionare l'immagine da aggiungere al report dall'elenco a discesa. Fare clic sul pulsante **Importa** per aggiungere l'immagine all'elenco a discesa.  
  
 Se si seleziona l'opzione **Esterna** , digitare l'URL dell'immagine. Per un report pubblicato in un server di report configurato per la modalità nativa, utilizzare un percorso completo o relativo. Ad esempio, http://\<ServerName>/images/image1.jpg. Per un report pubblicato in un server di report configurato per la modalità integrata SharePoint, utilizzare un URL completo. Ad esempio, http://\<*NomeSharePointServer*>/\<*sito*>/Documents/images/image1.jpg.  
  
 **Importa**  
 Fare clic su questa opzione per aggiungere un'immagine all'elenco a discesa **Use this image** (Usa questa immagine).  
  
 **Utilizzare questo campo**  
 Questa opzione viene visualizzata se si seleziona l'opzione **Database** . Selezionare il nome del campo.  
  
 **Utilizzare questo tipo MIME**  
 Scegliere il formato appropriato delle immagini contenute nel database, ad esempio bmp, jpeg, gif, png e x-png.  
  
## <a name="see-also"></a>Vedi anche  
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Immagini &#40;Generatore report e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Guida di Generatore report per finestre di dialogo, riquadri e procedure guidate](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
