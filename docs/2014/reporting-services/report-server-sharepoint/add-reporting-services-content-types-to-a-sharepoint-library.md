---
title: Aggiungere la Web Part Visualizzatore Report a una pagina Web (Reporting Services in modalità integrata SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: cac75345-2380-467d-a394-0a2140908a5a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 468acea55c334ffda169daff2b5da4c417348a3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104285"
---
# <a name="add-the-report-viewer-web-part-to-a-web-page-reporting-services-in-sharepoint-integrated-mode"></a>Aggiungere la web part Visualizzatore report a una pagina Web (Reporting Services in modalità integrata SharePoint)
  È possibile utilizzare la web part Visualizzatore report per visualizzare report eseguiti in un server di report configurato per l'esecuzione in modalità integrata SharePoint. Questa web part può essere utilizzata per visualizzare i file di definizione dei report (con estensione rdl) creati in Generatore report o Progettazione report e caricati in una raccolta.  
  
 È possibile aggiungere la web part Visualizzatore report a una pagina Web se si desidera incorporare un report nella pagina.  
  
> [!NOTE]  
>  Sebbene abbiano lo stesso nome, la web part Visualizzatore report installata tramite il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è diversa dalla web part Visualizzatore report inclusa nel file RSWebParts.cab. Le istruzioni contenute in questo argomento sono specifiche della web part visualizzatore di report installata attraverso il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Per aggiungere una web part a una pagina Web, è necessario disporre dell'autorizzazione Aggiunta e personalizzazione pagine a livello di sito. Se si usano impostazioni di sicurezza predefinite, questa autorizzazione è concessa ai membri del gruppo **Proprietari** che hanno il livello di autorizzazione Controllo completo.  
  
### <a name="to-embed-a-report-in-a-web-page"></a>Per incorporare un report in una pagina Web  
  
1.  Aprire o creare il dashboard o la pagina web part.  
  
2.  Nella pagina **Azioni sito**fare clic su **Modifica pagina**.  
  
3.  Fare clic su **Aggiungi web part**.  
  
4.  Nell'elenco delle categorie di web part selezionare la categoria **Varie** e quindi selezionare **Visualizzatore report di SQL Server Reporting Services**.  
  
5.  Scegliere **Aggiungi**. La web part verrà aggiunta nella parte superiore dell'area. È possibile trascinarla in una posizione diversa all'interno dell'area.  
  
6.  Nel visualizzatore fare clic su **Fare clic qui per aprire il riquadro Strumenti**.  
  
7.  Fare clic sul pulsante per la ricerca ( **...** ) e selezionare un report da una raccolta della raccolta siti corrente. In alternativa è possibile digitare l'URL del report. Per determinare l'URL di un report, fare clic con il pulsante destro del mouse sul report e scegliere **Proprietà**. Non fare clic sulla freccia verso il basso visualizzata accanto al report. L'URL del report non è indicato nella pagina Visualizza proprietà dell'elemento. Se si copia e si incolla l'URL dalla finestra di dialogo **Proprietà** , sostituire con uno spazio tutte le occorrenze del codice "%20" presenti nell'URL. Ad esempio, modificare "Vendite%20azienda" in "Vendite azienda".  
  
    > [!NOTE]  
    >  Ogni web part Visualizzatore report può contenere un solo report. L'URL deve essere costituito dal percorso completo di un report presente nel sito di SharePoint corrente oppure in un sito disponibile nella stessa farm o applicazione Web. L'URL deve corrispondere a una raccolta documenti o a una cartella all'interno della raccolta documenti che contiene il report e deve includere l'estensione rdl del file. Se il report dipende da un file modello o di origine dati condivisa, non sarà necessario specificare tali file nell'URL, perché il report contiene riferimenti a tutti i file necessari.  
  
8.  Quando il riquadro Strumenti è aperto è possibile impostare alcune proprietà per modificare il layout e l'aspetto predefiniti.  
  
9. Fare clic sul pulsante **Applica** , disponibile nella parte inferiore del riquadro Strumenti, e quindi scegliere **OK** per chiudere il riquadro.  
  
## <a name="see-also"></a>Vedere anche  
 [Web part Visualizzatore report in un sito di SharePoint](../report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizzare la web part Visualizzatore report](../customize-the-report-viewer-web-part.md)   
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](../security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Installare o disinstallare il Reporting aggiuntivo Services per SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
