---
title: Il caricamento dei dati (aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b628548b-982b-4e45-abf4-c8e83e3ab1c2
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 465b14ab5cb96f3f587222427ea793bbaf225b01
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62923920"
---
# <a name="loading-data-mds-add-in-for-excel"></a>Caricamento dei dati (componente aggiuntivo MDS per Excel)
  Nel [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], è necessario caricare dati dal repository MDS in un foglio di lavoro di Excel attivo prima di lavorare con esso. Una volta completato l'utilizzo dei dati, pubblicarlo sul repository MDS in modo che altri utenti possano condividerlo.  
  
 I dati che è possibile caricare sono limitati ai dati per i quali si dispone dell'autorizzazione di accesso. L'autorizzazione di accesso ai dati viene impostata nell'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] o impostata a livello di programmazione.  
  
 Quando si caricano grandi quantità di dati, è possibile impostare avvisi che vengono visualizzati quando i dati potrebbero richiedere molto tempo per il caricamento. A tale scopo, nel gruppo **Opzioni** fare clic su **Impostazioni**. Nella scheda **Dati** selezionare **Visualizza avviso di filtro per grandi set di dati**.  
  
> [!WARNING]  
>  Una cartella di lavoro abilitata per MDS deve essere aperta e aggiornata solo in Excel con il componente aggiuntivo MDS per Excel. L'apertura di una cartella di lavoro abilitata per MDS in Excel su un computer nel quale non è installato il componente aggiuntivo Excel di MDS non è supportata e potrebbe provocare danni al file della cartella di lavoro. Se si desidera condividere dati con altri utenti, inviare tramite posta elettronica un file di query di collegamento a questi ultimi, anziché salvare il foglio di lavoro e inviarlo tramite posta elettronica. Per altre informazioni sulla query, vedere [Inviare tramite posta elettronica un file di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](email-a-shortcut-query-file-mds-add-in-for-excel.md).  
  
## <a name="filtering-data"></a>Filtro dei dati  
 È possibile filtrare i dati prima del caricamento per limitare la quantità di dati che si desidera scaricare. Ciò presuppone la scelta degli attributi (colonne) da caricare, l'ordine con cui si desidera visualizzare gli attributi e i membri (righe di dati) che si desidera utilizzare. Per altre informazioni, vedere [filtrare i dati prima del caricamento &#40;il componente aggiuntivo MDS per Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md).  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>Connettersi automaticamente e caricare i dati utilizzati frequentemente  
 Se si desidera connettersi sempre allo stesso server e caricare lo stesso set di dati, è possibile creare file di query collegamento che contengano la connessione e filtrino le informazioni. Per altre informazioni sui file di query, vedere [File di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](shortcut-query-files-mds-add-in-for-excel.md).  
  
## <a name="refreshing-data"></a>Aggiornamento dei dati  
 I dati nel repository MDS possono essere aggiornati dagli altri utenti dopo il caricamento. È possibile recuperare questi dati senza perdere le modifiche apportate a dati diversi da MDS. Per altre informazioni, vedere [Aggiornamento dei dati &#40;Componente aggiuntivo MDS per Excel&#41;](refreshing-data-mds-add-in-for-excel.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Filtrare i dati MDS prima di caricarli in Excel.|[Filtrare i dati prima del caricamento &#40;componente aggiuntivo MDS per Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)|  
|Caricare dati MDS in Excel.|[Caricare i dati da MDS in Excel](export-data-to-excel-from-master-data-services.md)|  
|Modificare l'ordine delle colonne prima di scaricare i dati.|[Riordinare le colonne &#40;componente aggiuntivo MDS per Excel&#41;](reorder-columns-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Connessioni &#40;componente aggiuntivo MDS per Excel&#41;](connections-mds-add-in-for-excel.md)  
  
-   [File di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Componente aggiuntivo Master Data Services per Microsoft Excel](master-data-services-add-in-for-microsoft-excel.md)  
  
-   [Sicurezza &#40;Master Data Services&#41;](../security-master-data-services.md)  
  
  
