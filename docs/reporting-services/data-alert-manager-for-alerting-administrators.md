---
title: Gestione avvisi dati per gli amministratori di avvisi | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: 32fd968f-1c0c-4ba8-851c-8a3b5e1fbbf2
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: a80b90f30ce2b304bd7bbb0229f172407589d3c9
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571547"
---
# <a name="data-alert-manager-for-alerting-administrators"></a>Gestione avvisi dati per gli amministratori di avvisi

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services include Gestione avvisi dati per consentire agli amministratori di avvisi di SharePoint di gestire gli avvisi dati. Gli amministratori di avvisi possono visualizzare le informazioni relative a tutti gli avvisi salvati nel sito, nonché eliminare avvisi. Nella figura seguente sono illustrate le funzionalità disponibili per i responsabili di avvisi di SharePoint tramite Gestione avvisi dati.

![Gestione avvisi per gli amministratori del sito di SharePoint](../reporting-services/media/rs-alertmanagersite.gif "Gestione avvisi per gli amministratori del sito di SharePoint")

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

 Quando il sito è abilitato per gli avvisi dati, vengono create e aggiunte al sito di SharePoint due pagine, ovvero MyDataAlerts.aspx e SiteDataAlerts.aspx. SiteDataAlerts.aspx rappresenta Gestione avvisi dati per gli amministratori di avvisi. Gli amministratori di avvisi possono aprire Gestione avvisi dati dalla pagina Impostazioni sito di SharePoint. Per aprire Gestione avvisi dati, gli amministratori di avvisi devono disporre dell'autorizzazione Gestione avvisi di SharePoint.  
  
 È inoltre possibile aprire Gestione avvisi dati direttamente utilizzando un URL. Di seguito è illustrata la sintassi dell'URL:  
  
 `http: //<site name>/_layouts/ReportServer/ SiteDataAlerts.aspx`  
  
> [!NOTE]  
>  Un amministratore di avvisi può concedere agli Information Worker l'autorizzazione per accedere alle funzionalità di avviso dati di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Per informazioni sulle autorizzazioni richieste, vedere [Avvisi dati di Reporting Services](../reporting-services/reporting-services-data-alerts.md).  
  
##  <a name="ViewingAlerts"></a> Visualizzazione delle informazioni sugli avvisi dati  
 Se Reporting Services viene installato e configurato in SharePoint, nella pagina Impostazioni sito di SharePoint sono incluse le opzioni di **Reporting Services** . Per aprire Gestione avvisi dati, gli amministratori di avvisi possono fare clic sull'opzione **Gestisci avvisi dati** disponibile in Reporting Services. Nella figura seguente viene illustrata la posizione nella pagina Impostazioni sito da cui è possibile aprire Gestione avvisi dati.  
  
 ![Sezione Reporting Services della pagina Impostazioni sito](../reporting-services/media/rs-sitesettings.gif "Sezione Reporting Services della pagina Impostazioni sito")  
  
 In Gestione avvisi dati è inclusa una tabella in cui sono elencati il nome dell'avviso, il nome del report, il nome del proprietario dell'avviso, il numero di volte in cui il messaggio di avviso è stato inviato, l'ultima esecuzione dell'avviso, l'ultima modifica alla definizione di avviso e lo stato del messaggio di avviso. Se l'avviso non può essere generato o inviato, nella colonna relativa allo stato sono incluse informazioni sull'errore che consentono di risolvere i problemi relativi all'avviso. Per altre informazioni, vedere [Gestire tutti gli avvisi dati in un sito di SharePoint con Gestione avvisi dati](../reporting-services/manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md).  
  
 Nella tabella seguente sono illustrati i dati di esempio di una tabella di Gestione avvisi dati. Quando si verifica un errore, il messaggio di errore e l'identificatore della voce nel log (un GUID) vengono inclusi nel campo **Stato** nella tabella.  
  
|Nome dell'avviso|Nome del report|Creato da|Avvisi inviati|Ultima esecuzione|Data ultima modifica|Stato|  
|----------------|-----------------|----------------|-----------------|--------------|-------------------|------------|  
|SalesQTR|SalesByTerritoryAndQTR|Lauren Johnson|4|6/12/2011|6/1/2011|L'ultimo avviso è stato eseguito correttamente e l'avviso è stato inviato.|  
|UnitsSold|ProductsSalesByQTR|Michael Blythe|2|7/1/2011|6/28/2011|L'ultimo avviso è stato eseguito correttamente, tuttavia i dati non sono stati modificati e non è stato inviato alcun avviso.|  
|InventoryCount|StockStatusByQTR|Lauren Johnson|7|7/10/2011|7/2/2011|\<messaggio di errore>Il file di log contiene informazioni dettagliate sull'errore. Fare riferimento alla voce del log con l'identificatore: \<GUID>.|  
|TopPromotion|PromotionTracking|Cristian Petculescu|0||5/23/2011|Avviso creato.|  
  
 Per altre informazioni, vedere [Gestire tutti gli avvisi dati in un sito di SharePoint con Gestione avvisi dati](../reporting-services/manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md).  
  
 È possibile visualizzare tutti gli avvisi creati dagli utenti del sito. È necessario scegliere un utente, quindi scegliere se visualizzare tutti i relativi avvisi o solo quelli per un report specifico.  
  
  
##  <a name="DeleteAlerts"></a> Eliminare avvisi dati  
 Le definizioni di avviso dati vengono eliminate da Gestione avvisi dati. Ogni definizione di avviso dati dispone di un proprietario, ovvero l'utente di SharePoint da cui è stata creata. I proprietari possono eliminare solo le definizioni di avviso che hanno creato. Per altre informazioni, vedere [Gestire gli avvisi dati in Gestione avvisi dati](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md).  
  
 Gli amministratori di avvisi di SharePoint possono elencare e quindi eliminare le definizioni di avviso create da tutti gli utenti del sito. Per altre informazioni, vedere [Gestire tutti gli avvisi dati in un sito di SharePoint con Gestione avvisi dati](../reporting-services/manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md).  
  
 Dopo aver eliminato la definizione di avviso, non verranno inviati ulteriori avvisi. Se tuttavia si esegue una query sul database di avvisi, è possibile trovare ancora la definizione di avviso. Il servizio avvisi consente di eseguire la pulizia in base a una pianificazione e la definizione di avviso verrà eliminata definitivamente alla successiva operazione di pulizia. L'intervallo di pulizia predefinito è impostato su 20 minuti. Questo e altri intervalli di pulizia sono configurabili. Per altre informazioni, vedere [Avvisi dati di Reporting Services](../reporting-services/reporting-services-data-alerts.md).  
  
  
##  <a name="HowTo"></a> Attività correlate  
 In questa sezione è elencata una procedura tramite cui viene illustrata la modalità di gestione degli avvisi.  
  
-   [Gestire tutti gli avvisi dati in un sito di SharePoint con Gestione avvisi dati](../reporting-services/manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)  

## <a name="see-also"></a>Vedere anche

[Avvisi dati di Reporting Services](../reporting-services/reporting-services-data-alerts.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
