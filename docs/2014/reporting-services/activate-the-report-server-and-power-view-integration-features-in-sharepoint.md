---
title: Attivare il server di report e Power View le funzionalità di integrazione in SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c7f64a54-c555-4d31-bf99-3abe57dc8626
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e30ae6ea0e7fa314748c4da265650273c0a7d56e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66110030"
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>Attivare le funzionalità di integrazione per Power View e server di report in SharePoint
  Le [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] funzionalità della raccolta siti vengono in genere attivate per impostazione predefinita [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] dopo l'installazione del componente aggiuntivo per prodotti SharePoint. In alcune situazioni sarà necessario attivare manualmente le funzionalità.  
  
 Se si installa il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per Prodotti SharePoint 2010 dopo l'installazione del prodotto SharePoint, la funzionalità di integrazione del server di report e la funzionalità di integrazione di Power View saranno attivate solo per le raccolte siti radice. Per le altre raccolte siti, sarà necessario attivare manualmente le funzionalità. Ad esempio, se è presente una raccolta siti **http://[nome server]/sites/[nome raccolta siti]** , sarà necessario attivare manualmente le funzionalità delle raccolte siti di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
 Se non è presente alcuna raccolta siti radice, il componente aggiuntivo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] registra un messaggio simile al seguente.  
  
 "L'applicazione Web SharePoint 80 non dispone della raccolta siti radice"  
  
 Il messaggio verrà trovato nel log di installazione del componente aggiuntivo, denominato "RS_SP_ #. log" dove # è un numero incrementale. Il file di log verrà trovato nella cartella temporanea utenti correnti, ad esempio C:\Users\\[nome utente] \AppData\Local\Temp. Per ulteriori informazioni sulle opzioni di registrazione con il componente aggiuntivo, vedere [installare o disinstallare il componente aggiuntivo Reporting Services per sharepoint &#40;sharepoint 2010 e sharepoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  
  
 In questo argomento  
  
-   [Per attivare il server di report e le funzionalità di raccolta siti di integrazione Power View:](#bkmk_features)  
  
-   [Per attivare o disattivare Reporting Services funzionalità raccolta siti di amministrazione centrale:](#bkmk_centraladmin)  
  
##  <a name="bkmk_features"></a>Per attivare il server di report e le funzionalità di raccolta siti di integrazione Power View:  
  
1.  Aprire il browser al sito dove si desidera che le funzionalità [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] siano attive.  
  
2.  Fare clic su **Azioni sito**.  
  
3.  Fare clic su **Impostazioni sito**.  
  
4.  Fare clic su **Funzionalità raccolta siti** nel gruppo Amministrazione raccolta siti  
  
5.  Individuare **Funzionalità di integrazione Server report** o **Funzionalità di integrazione Power View** nell'elenco.  
  
6.  Fare clic su **Attiva**.  
  
 Per disattivare le funzionalità, è possibile utilizzare la stessa procedura facendo clic su **Disattiva** anziché su **Attiva**.  
  
##  <a name="bkmk_centraladmin"></a>Per attivare o disattivare Reporting Services funzionalità raccolta siti di amministrazione centrale:  
  
1.  Aprire il browser alla pagina Amministrazione centrale SharePoint.  
  
2.  Fare clic su **Azioni sito**.  
  
3.  Fare clic su **Impostazioni sito**.  
  
4.  Fare clic su **Funzionalità raccolta siti** nel gruppo Amministrazione raccolta siti  
  
5.  Individuare **Funzionalità Amministrazione centrale del server di report** nell'elenco.  
  
6.  Fare clic su **Attiva**.  
  
 Per disattivare la funzionalità, è possibile utilizzare la stessa procedura facendo tuttavia clic su **Disattiva** anziché su **Attiva.**  
  
## <a name="next-steps"></a>Passaggi successivi  
 Dopo aver attivato la funzionalità, è possibile continuare con l'integrazione del server.  
  
## <a name="see-also"></a>Vedere anche  
 [Installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
