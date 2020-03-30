---
title: Migrazione dalla modalità nativa alla modalità SharePoint | Microsoft Docs
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: c5b15bec-6fde-4174-bcde-d043307244dd
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4ae49e1110a1d539cbe7095f946be7fc522b80b1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082619"
---
# <a name="native-to-sharepoint-migration-ssrs"></a>Migrazione dalla modalità nativa alla modalità SharePoint (SSRS)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Non è possibile eseguire l'aggiornamento o la conversione da una modalità server all'altra di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Non è possibile, ad esempio, eseguire l'aggiornamento o la conversione da un server di report in modalità nativa a un server di report in modalità SharePoint. Non è possibile copiare i database del server di report tra modalità poiché in essi vengono utilizzati schemi del database diversi. È possibile eseguire la migrazione del contenuto da un server di report a un altro. Gli strumenti utilizzati dipendono dal tipo di modalità del server di report configurata per il server di origine e di destinazione.  
  
##  <a name="reporting-services-migration-tool"></a><a name="bkmk_native_to_sharepoint"></a> Strumento di migrazione di Reporting Services  
 Lo strumento supporta la migrazione del contenuto da una distribuzione in modalità nativa a una distribuzione in modalità SharePoint. Lo strumento non supporta la migrazione dalla modalità SharePoint alla modalità SharePoint o dalla modalità SharePoint alla modalità nativa.  
  
 Per altre informazioni, vedere la pagina relativa allo [strumento di migrazione di Reporting Services](https://www.microsoft.com/download/details.aspx?id=29560) (https://www.microsoft.com/download/details.aspx?id=29560).  
  
## <a name="use-script-to-migrate-content"></a>Utilizzare lo script per eseguire la migrazione di contenuto  
 Se lo strumento di migrazione non soddisfa le proprie esigenze, è possibile eseguire manualmente la migrazione dei dati del server di report. Di seguito è riportato un riepilogo dei passaggi necessari per eseguire la migrazione degli elementi del report da una distribuzione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a un'altra. L'approccio supporta la modalità nativa o la modalità SharePoint come server di origine o di destinazione.  
  
1.  Eseguire il backup e il ripristino delle chiavi di crittografia. Si tratta della chiave utilizzata per crittografare i dati. La chiave di crittografia viene utilizzata anche per crittografare le password, ad esempio le password archiviate per le connessioni alle origini dati. Tuttavia, non è possibile eseguire la migrazione delle password e sarà necessario immetterle nuovamente nell'ambiente di destinazione.  
  
2.  **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Script RSS:** Scrivere uno script Visual Basic per chiamare i metodi SOAP del servizio Web ReportServer per copiare i dati tra database. Utilizzare l'utilità **RS.exe** per eseguire lo script. RS.exe viene installato con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
    -   [Script di esempio rs.exe di Reporting Services per la copia di contenuto tra server di report](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md). Gli argomenti illustrano come utilizzare lo script di esempio che è possibile scaricare da CodePlex.  
  
    -   Script RSS di esempio disponibile da CodePlex, [Script di Reporting Services RS.exe che esegue la migrazione del contenuto da un server di report a un altro](https://azuresql.codeplex.com/releases/view/115207).+  
  
    -   [Script e PowerShell con Reporting Services](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md)  
  
 Nella tabella seguente vengono riepilogati gli oggetti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] di cui è possibile eseguire la migrazione con gli script:  
  
|Oggetto|Esecuzione dello script|Commenti|  
|------------|---------------------|--------------|  
|Report|Sì|Al termine della migrazione immettere nuovamente le password per le origini dati.|  
|Datasources|Sì|Al termine della migrazione collegare nuovamente i report alle origini dati.|  
|Modelli|Sì||  
|Set di dati|Sì||  
|Parti del report||Al termine della migrazione verificare o aggiornare il percorso alle parti del report.|  
|Pianificazioni|Sì|Vedere il metodo ListSchedules in [Subscription and Delivery Methods](../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md).|  
|Sottoscrizioni|sì|Vedere il metodo ListSubscriptions in [Subscription and Delivery Methods](../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md) e il metodo <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A> .|  
|Snapshot|||

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
