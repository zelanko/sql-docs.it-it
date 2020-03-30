---
title: Prenotazioni URL per le distribuzioni di più istanze del server di report | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: f67c83c0-1f74-42bb-bfc1-e50c38152d3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0a09d7c391af0d8800f5d9c66d40ab7ba0c2cbf4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "62513283"
---
# <a name="url-reservations-for-multi-instance-report-server-deployments"></a>Prenotazioni URL per le distribuzioni di più istanze del server di report
  Se si installano più istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nello stesso computer, è necessario prendere in considerazione le modalità di prenotazione degli URL per ogni istanza. All'interno di ogni istanza, il servizio Web ReportServer e [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] devono disporre almeno di una prenotazione URL ciascuno. L'intero set di prenotazioni deve essere univoco in HTTP.SYS.  
  
 Eventuali URL duplicati vengono rilevati durante la registrazione dell'URL che viene eseguita all'avvio del servizio. Se si creano prenotazioni URL non univoche, il conflitto di nome potrebbe non essere rilevato fino all'avvio del servizio. Per questa ragione, verificare che si seguano regole o convenzioni di denominazione o regole per garantire che tutti i valori siano univoci.  
  
## <a name="default-naming-conventions"></a>Convenzioni di denominazione predefinite  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] può essere installato all'interno di un'istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando si installa o si configura un server di report all'interno di un'istanza denominata, il nome dell'istanza viene incluso automaticamente nella directory virtuale nella prenotazione URL predefinita specificata da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Nella tabella seguente vengono illustrate le prenotazioni URL per un'istanza predefinita e per un'istanza denominata.  
  
|Istanza di SQL Server|Prenotazioni URL predefinita|  
|-------------------------|-----------------------------|  
|Predefinita (MSSQLSERVER)|`https://+:80/reportserver`|  
|Denominata (Istanzadenominatautente)|`https://+:80/reportserver_MyNamedInstance`|  
  
 Per l'istanza denominata, la directory virtuale include il nome dell'istanza. Sia l'istanza predefinita che quella denominata restano in attesa sulla stessa porta, ma i nomi delle directory virtuali univoci determinano il server di report che ottiene la richiesta.  
  
 È consigliabile utilizzare il nome della directory virtuale per effettuare una distinzione tra le istanza del server di report. Tale nome fornisce una corrispondenza chiara tra un URL e l'istanza di destinazione e assicura che i nomi delle applicazioni siano univoci in tutto il sistema.  
  
## <a name="custom-naming-conventions"></a>Convenzioni di denominazione personalizzate  
 Anche se è consigliabile utilizzare il nome dell'istanza, è possibile utilizzare la sintassi dell'URL e convenzioni di denominazione personalizzate per soddisfare i vincoli relativi al nome univoco per le prenotazioni URL. Negli esempi seguenti vengono illustrati approcci diversi per la creazione di URL univoci per ogni istanza.  
  
|Istanza predefinita di un server di report (MSSQLSERVER)|ReportServer_Istanzadenominatautente|Univocità|  
|----------------------------------------------------|-----------------------------------|----------------|  
|`https://+:80/reportserver`|`https://+:8888/reportserver`|Ogni istanza resta in attesa su una porta diversa.|  
|`https://www.contoso.com/reportserver`|`https://SRVR-46/reportserver`|Ogni istanza risponde a nomi di server diversi (nome completo di dominio e nome del computer).|  
  
## <a name="uniqueness-requirements"></a>Requisiti di univocità  
 Le tecnologie sottostanti utilizzate da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] impongono alcuni requisiti relativi ai nomi univoci. Per HTTP.SYS è necessario che tutti gli URL all'interno del relativo repository siano univoci. È possibile variare la porta, il nome host o nome della directory virtuale per creare un URL univoco. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] è necessario che le identità dell'applicazione siano univoche all'interno dello stesso processo. Questo requisito influisce sui nomi delle directory virtuali, poiché specifica che non è possibile duplicare un nome di directory virtuale all'interno della stessa istanza del server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurare un URL &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
