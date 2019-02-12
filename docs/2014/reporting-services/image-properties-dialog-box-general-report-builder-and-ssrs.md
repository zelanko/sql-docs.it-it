---
title: Immagine di finestra di dialogo proprietà, generale (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10051"
- sql12.rtp.rptdesigner.pictureproperties.general.f1
ms.assetid: c2218b93-f7fe-46ef-995f-d7dadf9752ec
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: cbbe4fe5917419bc07cef81629c7b2e38b7cff15
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019637"
---
# <a name="image-properties-dialog-box-general-report-builder-and-ssrs"></a>Finestra di dialogo Proprietà immagine, Generale (Generatore report e SSRS)
  Selezionare **Generale** nella finestra di dialogo **Proprietà immagine** per aggiungere un'immagine, modificare il nome predefinito dell'immagine e aggiungere il testo della descrizione comando.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Digitare un nome per l'elemento. Il nome deve essere univoco nel report. Per impostazione predefinita, viene assegnato un nome generale, ad esempio Immagine1 o Immagine2.  
  
 **Descrizione comando**  
 Digitare un testo o un'espressione che restituisca una descrizione comando. Fare clic sul pulsante Espressione (*fx*) per modificare l'espressione. Il **descrizione comando** appare quando l'utente mette in pausa il puntatore sull'elemento in un report HTML.  
  
 **Selezionare l'origine dell'immagine**  
 Indicare il percorso di archiviazione dell'immagine in modo da specificare da dove il componente Elaborazione report recupererà l'immagine durante il rendering del report.  
  
-   **Esterna** Scegliere questa opzione se si desidera che l'immagine continui ad essere disponibile come file su un server di report o un server Web.  
  
-   **Incorporata** Scegliere questa opzione se si desidera incorporare l'immagine nel report.  
  
-   **Database** Scegliere questa opzione se si desidera includere un nome di campo del database che rappresenti le immagini da includere nel report.  
  
 **Usare questa immagine**  
 Questa opzione viene visualizzata quando si seleziona l'opzione **Incorporata** o **Esterna** .  
  
 Se si intende incorporare l'immagine, selezionare l'immagine da aggiungere al report dall'elenco a discesa. Fare clic sul pulsante **Importa** per aggiungere l'immagine all'elenco a discesa.  
  
 Se si seleziona l'opzione **Esterna** , digitare l'URL dell'immagine. Per un report pubblicato in un server di report configurato per la modalità nativa, utilizzare un percorso completo o relativo. Ad esempio, http://\<nomeserver > / Images/immagine1.jpg. Per un report pubblicato in un server di report configurato per la modalità integrata SharePoint, utilizzare un URL completo. Ad esempio, http://\<*NomeServerSharePoint*>/\<*sito*> / Documents/images/image1.jpg.  
  
 **Importa**  
 Fare clic su questa opzione per aggiungere un'immagine all'elenco a discesa **Use this image** (Usa questa immagine).  
  
 **Usare questo campo**  
 Questa opzione viene visualizzata se si seleziona l'opzione **Database** . Selezionare il nome del campo.  
  
 **Utilizzare questo tipo MIME**  
 Scegliere il formato appropriato delle immagini contenute nel database, ad esempio bmp, jpeg, gif, png e x-png.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Immagini &#40;Generatore report e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Guida di Generatore report per finestre di dialogo, riquadri e procedure guidate](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
