---
title: Aggiungere parametri a un report per dispositivi mobili | Reporting Services | Microsoft Docs
ms.date: 07/30/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 113cb057-deec-40eb-abc8-f35d3900eaa6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 348a8c1fa8ccdb4ade5b2ee3d39d6ecacf6e5a03
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "63317087"
---
# <a name="add-parameters-to-a-mobile-report--reporting-services"></a>Aggiungere parametri a un report per dispositivi mobili | Reporting Services
È possibile creare un report per dispositivi mobili di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] con parametri in modo che l'autore e i lettori dei report possano filtrare i report stessi. Un report con parametri può essere anche la destinazione di un [drill-through da un report di origine](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md). 

Per creare un report per dispositivi mobili con parametri, iniziare con un set di dati condiviso con almeno un parametro. Per altre informazioni, vedere [Creare un set di dati condiviso o un set di dati incorporato (Generatore report e SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md). I report per dispositivi mobili non supportano valori null per i parametri predefiniti, quindi verificare che i parametri abbiano valori predefiniti diversi da null.

Dopo aver aggiunto i parametri a un report per dispositivi mobili, creare un URL per [aprire il report con parametri della stringa di query](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md). 

1. Nella barra superiore del portale Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] selezionare **Nuovo** > **Report per dispositivi mobili**.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. Selezionare la scheda **Dati** nell'angolo in alto a sinistra di [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)].   
  
3. Selezionare **Aggiungi dati**nell'angolo in alto a destra.  
  
4. Selezionare **Server di report**e quindi selezionare un server.  
  
5. Passare ai set di dati condivisi sul server e selezionarne uno dotato di parametri.  
  
   I dati del set di dati vengono visualizzati nella griglia. Il cerchio verde con parentesi graffe **{ }** contrassegna un set di dati con un parametro.  
     
   ![SSMRP_PforParam](../../reporting-services/mobile-reports/media/ssmrp-pforparam.png)  
  
6. Fare clic sulla ruota visualizzata sulla scheda e quindi selezionare **Param{}** .  
  
   ![SSMRP_ParamWheel](../../reporting-services/mobile-reports/media/ssmrp-paramwheel.png)  
  
7. Selezionare l'elemento di report che passerà i valori al parametro.  
  
   ![SSMRP_SetParam](../../reporting-services/mobile-reports/media/ssmrp-setparam.png)  
     
8. Selezionare **Anteprima** per visualizzare l'aspetto del report. In questo report l'elenco di selezione usa il parametro di categoria.

   ![sql-server-mobile-report-publisher-Selection-List-View-No-Selection](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-view-no-selection.png) 
   
9. Quando si seleziona un valore nell'elenco di selezione, il report viene filtrato per tale valore. In questo caso, Accessori.

   ![sql-server-mobile-report-publisher-Selection-List-Category-Selected](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-category-selected.png)   
  
### <a name="see-also"></a>Vedere anche  
-  [Aprire un report per dispositivi mobili con parametri della stringa di query specifici](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md)
-  [Aggiungere il drill-through da un report per dispositivi mobili ad altri report per dispositivi mobili o URL](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)
-  [Creare un set di dati condiviso o un set di dati incorporato](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)
- [Creare e pubblicare report per dispositivi mobili con SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  

