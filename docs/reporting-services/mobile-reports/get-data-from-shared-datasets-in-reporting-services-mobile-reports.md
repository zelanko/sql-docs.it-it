---
title: Ottenere dati da un set di dati condivisi nei report di Reporting Services per dispositivi mobili | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 0b846451-c8d0-412c-802d-a42bb1ff8c63
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cac1a32b49fde5b41c0a8ef21706d873ce037cd3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "63061153"
---
# <a name="get-data-from-shared-datasets-in-reporting-services-mobile-reports"></a>Ottenere dati da un set di dati condivisi nei report di Reporting Services per dispositivi mobili
Oltre a [caricare dati da file di Excel](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md), SQL Server Mobile Report Publisher può anche accedere ai dati di quasi tutte le origini. L'accesso ai dati richiede un'origine dati condivisa, configurata in un portale Web di Reporting Services. Altre informazioni sulla [creazione di origini dati condivise](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) e sulla [creazione di set di dati condivisi](../../reporting-services/report-data/manage-shared-datasets.md).  
  
Dopo avere configurato le origini dati condivise e i set di dati condivisi nel server di Reporting Services, è possibile usarli nei report per dispositivi mobili creati in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].   
  
Una volta stabilita la connessione a un server [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] da [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)], è semplice definire la connessione di un report per dispositivi mobili a un set di dati condivisi.   
  
1. Nella scheda **Dati** selezionare **Aggiungi dati**.  
  
2. Selezionare **Server di report**.   
  
3.  Se è la prima volta che ci si connette al server, specificare il nome del server e il proprio nome e la propria password. Inserire il nome del server nella casella Indirizzo server usando il formato seguente:  
  
    \<"nomeserver">/reports/  
  
    Come in questo esempio:  
       
    ![SSMRP_ConnectToServer](../../reporting-services/mobile-reports/media/ssmrp-connecttoserver.png)  
      
  
4. Quando si seleziona il server [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] , vengono visualizzati i set di dati disponibili nelle cartelle. Selezionare un set di dati per importare i dati in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
   ![SS_MRP_ServerData](../../reporting-services/mobile-reports/media/ss-mrp-serverdata.png)  
  
Dopo aver importato il set di dati, è possibile progettare il report per dispositivi mobili come si farebbe con dati simulati o dati locali da un file di Excel.  
  
Per impostazione predefinita, il set di dati condiviso è sempre aggiornato con i dati più recenti perché ogni volta che un utente visualizza un report per dispositivi mobili basato su set di dati, SQL Server esegue la query sottostante e restituisce i dati più recenti. Ovviamente, se il report per dispositivi mobili viene visualizzato da molte persone questa potrebbe non essere la soluzione ideale, quindi è possibile impostare la memorizzazione nella cache per eseguire periodicamente la query e memorizzare nella cache il set di dati risultante. Questo post di blog spiega [come funziona la memorizzazione nella cache e l'aggiornamento dei dati nel portale Web](https://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/).  
  
## <a name="add-edit-or-remove-a-report-server"></a>Aggiungere, modificare o rimuovere un server di report  
  
Se si è già connessi a un server di report, quando si seleziona **Aggiungi dati** nella scheda Dati, l'opzione per aggiungere un altro server di report non è visibile. In alternativa, eseguire questa procedura.  
  
1. Nell'angolo in alto a sinistra selezionare **Connessioni**.  
  
   ![SSMRP_AddConnectionIcon](../../reporting-services/mobile-reports/media/ssmrp-addconnectionicon.png)  
     
   A destra viene visualizzato il riquadro Connessioni server.  
     
   ![SSMRP_ServerConnectnPane](../../reporting-services/mobile-reports/media/ssmrp-serverconnectnpane.png)  
     
2. Aggiungere una nuova connessione server oppure modificare o rimuovere quelle esistenti.  
  
### <a name="see-also"></a>Vedere anche  
- [Creare e pubblicare report per dispositivi mobili con SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [Portale Web (modalità nativa SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)  
-  Vedere [Visualizzare report per dispositivi mobili e indicatori KPI di SQL Server nell'app iPad](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI per iOS)  
-  [Visualizzare report per dispositivi mobili e indicatori KPI di SQL Server nell'app iPhone](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI per iOS)  
  
  
  
  

