---
title: Connettere Part filtro o documenti Web (Reporting Services in modalità integrata SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Filter Web Part [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
- Documents Web Part [Reporting Services]
ms.assetid: 6a303135-c0ef-44cd-a423-1cea8df3dcf3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 062733f1ee68cd90ccc1b9a15d0cadc06b7e6f89
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109721"
---
# <a name="connect-filter-or-documents-web-part-reporting-services-in-sharepoint-integrated-mode"></a>Connettere una web part Filtro o Documenti (Reporting Services in modalità integrata SharePoint)
  Se si utilizza un prodotto SharePoint, è possibile creare un dashboard o una pagina web part in cui sono incluse una web part di filtro o una web part Documenti e una web part Visualizzatore report. Le versioni supportate sono [!INCLUDE[SPF2010](../includes/spf2010-md.md)] o [!INCLUDE[SPS2010](../includes/sps2010-md.md)]. Sono anche supportate le versioni [!INCLUDE[winSPServ3](../includes/winspserv3-md.md)] e [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007. Se si connette una web part di filtro, quando l'utente seleziona un valore di filtro in una web part di filtro, tale valore verrà inviato a un report con parametri nella stessa pagina. Se si connette una web part Documenti, quando l'utente fa clic su un report disponibile nella raccolta Documenti, tale report verrà visualizzato in una web part Visualizzatore report adiacente.  
  
 La web part di filtro consente di inviare valori a uno o più parametri di un report. È possibile utilizzare una web part di filtro solo con i report per cui sono definiti parametri compatibili con i valori, il tipo di dati e il formato inviati dalla web part.  
  
 La web part Documenti è associata alla raccolta Documenti del sito principale. Per visualizzare, aggiungere o rimuovere elementi dalla raccolta Documenti, fare clic su **Visualizza tutto il contenuto del sito**. In Raccolte fare clic su **Documenti**. Per gestire gli elementi della raccolta Documenti, è possibile usare i menu **Nuovo**, **Carica**e **Azioni** .  
  
### <a name="to-connect-a-filter-web-part"></a>Per connettere una web part di filtro  
  
1.  Aprire o creare il dashboard o la pagina web part.  
  
2.  Scegliere **Modifica pagina** dal menu **Azioni sito**.  
  
3.  Fare clic su **Aggiungi web part**.  
  
4.  Nella categoria **Varie**di **Tutte le web part** selezionare **Visualizzatore report di SQL Server Reporting Services**.  
  
5.  Scegliere **Aggiungi**. La web part verrà aggiunta nella parte superiore dell'area.  
  
6.  In un'altra area dello stesso dashboard o pagina web part fare clic su **Aggiungi web part**.  
  
7.  Nella sezione **Filtri**di **Tutte le web part** selezionare una web part.  
  
8.  Scegliere **Aggiungi**. La web part verrà aggiunta nella parte superiore dell'area.  
  
9. Nell'area che contiene la web part fare clic sul menu **Modifica** della web part, scegliere **Connessioni**, **Send Filter Values To**(Invia valori filtro a), quindi **Visualizzatore report** - *nome report*.  
  
10. Archiviare le modifiche e salvare la pagina.  
  
### <a name="to-connect-a-documents-web-part"></a>Per connettere una web part Documenti  
  
1.  Aprire o creare il dashboard o la pagina web part.  
  
2.  Scegliere **Modifica pagina** dal menu **Azioni sito**.  
  
3.  Fare clic su **Aggiungi web part**.  
  
4.  Nella sezione **Elenchi e raccolte**di **Tutte le web part** selezionare **Documenti**.  
  
5.  Scegliere **Aggiungi**. La web part verrà aggiunta nella parte superiore dell'area.  
  
6.  Fare clic sul pulsante **Applica** , disponibile nella parte inferiore del riquadro Strumenti, quindi scegliere **OK** per chiudere il riquadro.  
  
7.  In un'altra area dello stesso dashboard o pagina web part fare clic su **Aggiungi web part**.  
  
8.  Nella categoria **Varie**di **Tutte le web part** selezionare **Visualizzatore report di SQL Server Reporting Services.**  
  
9. Scegliere **Aggiungi**. La web part verrà aggiunta nella parte superiore dell'area.  
  
10. Nell'area che contiene la web part fare clic sul menu **Modifica** della web part, scegliere **Connessioni**, **Get report definitions from**(Recupera definizioni report da), quindi **Documenti**.  
  
11. Archiviare le modifiche e salvare la pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere la web part Visualizzatore report a una pagina Web &#40;Reporting Services in modalità integrata SharePoint&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)   
 [Web part Visualizzatore report in un sito di SharePoint](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizzare la web part Visualizzatore report](../../2014/reporting-services/customize-the-report-viewer-web-part.md)  
  
  
