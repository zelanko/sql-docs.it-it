---
title: Pubblicazione dei report in un server di report | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- production environments [Reporting Services]
- report projects [Reporting Services]
- Debug configuration [Reporting Services]
- report publishing [Reporting Services]
- publishing reports [Reporting Services]
- report properties [Reporting Services]
- Report Designer [Reporting Services], deploying reports
- Production configuration [Reporting Services]
- publishing reports [Reporting Services], production environments
- DebugLocal configuration [Reporting Services]
- deploying [Reporting Services], reports
- Report Designer [Reporting Services], publishing reports
ms.assetid: bd7aa5e0-61ce-43fd-8f74-5d1aeed078bb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5c73e75bbdf458b27d0f879a91e72ececc832b88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102490"
---
# <a name="publishing-reports-to-a-report-server"></a>Pubblicazione dei report in un server di report
  Dopo aver progettato e testato un report o un set di report, è possibile utilizzare le funzionalità di distribuzione predefinite di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per pubblicare i report in un server di report. sia singolarmente sia includendoli in un progetto server di report. La pubblicazione di un progetto server report è il modo più semplice per pubblicare più report. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Usa il termine *deploy*anziché il termine *Publish*. I due termini sono perfettamente equivalenti.  
  
 Per poter pubblicare un report, è necessario disporre delle autorizzazioni appropriate. L'autorizzazione è determinata dalla sicurezza basata sui ruoli definita dall'amministratore del server di report. In genere le operazioni di pubblicazione vengono concesse tramite il ruolo Server di pubblicazione.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] vengono fornite configurazioni del progetto per gestire la pubblicazione dei report. La configurazione specifica il percorso del server di report, la versione di SQL Server Reporting Services installata nel server di report, l'eventuale sovrascrittura delle origini dati pubblicate nel server di report e così via. Oltre a usare le configurazioni fornite in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , è possibile crearne di nuove.  
  
## <a name="project-configurations"></a>Configurazioni di progetto  
 I report vengono compilati prima della pubblicazione per garantire che nel server di report vengano pubblicate solo le definizioni dei report valide. Le configurazioni di progetto includono le proprietà per la compilazione dei report, ad esempio la cartella nella quale archiviare temporaneamente i report compilati e le modalità di gestione dei problemi di compilazione. Le configurazioni dispongono inoltre delle proprietà necessarie per specificare il percorso e la versione del server di report, nonché le cartelle sul server di report.  
  
 Per impostazione predefinita, in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sono disponibili tre configurazioni di progetto: DebugLocal, Debug e Release. La configurazione predefinita è DebugLocal. La configurazione DebugLocal viene usata in genere per visualizzare i report in una finestra di anteprima locale, la configurazione Debug per pubblicare i report in un server di prova e la configurazione Release per pubblicare i report in un server di produzione. Nell'elenco a discesa delle configurazioni della soluzione sulla barra degli strumenti Standard viene indicata la configurazione attiva. Per utilizzare una configurazione diversa, selezionarla dall'elenco.  
  
 Nell'ambiente di gestione dei report potrebbero essere installati più server di report e varie versioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . È possibile creare più configurazioni e utilizzarne quindi una diversa in base allo scenario di distribuzione. Per ulteriori informazioni, vedere [distribuzione e supporto della versione in SQL Server Data Tools &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md) e [impostare le proprietà di distribuzione &#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md).  
  
## <a name="publishing-reports"></a>Pubblicazione di report  
 È possibile pubblicare un singolo report o un progetto server di report che ne contenga più di uno. Per istruzioni sulla pubblicazione di report, vedere [pubblicare report](../publish-reports.md).  
  
### <a name="publishing-a-single-report"></a>Pubblicazione di un singolo report  
 Se non si desidera pubblicare tutti i report di un progetto, si può scegliere di pubblicarne anche uno soltanto. A tale scopo selezionare una configurazione che preveda la distribuzione del report, ad esempio la configurazione Release, fare clic con il pulsante destro del mouse sul report, quindi scegliere **Distribuisci**.  
  
 Se in un report viene utilizzata un'origine dati condivisa, è necessario distribuire anche tale origine. In caso contrario, il report distribuito non verrà eseguito. Fare clic con il pulsante destro del mouse sull'origine dati condivisa, quindi scegliere **Distribuisci**.  
  
 È necessario specificare l'URL del server di destinazione del server di report ed eventualmente modificare le cartelle predefinite nelle quali distribuire i report e le origini dati condivise.  
  
### <a name="publishing-multiple-reports"></a>Pubblicazione di più report  
 La pubblicazione di un progetto server di report implica la pubblicazione di tutti i report del progetto. Tutti i report vengono distribuiti utilizzando la stessa configurazione di progetto: lo stesso server di report, la stessa cartella sul server e così via. Affinché i report siano destinati a server diversi, è necessario pubblicarli uno alla volta oppure includere nel progetto server di report solo quelli desiderati. In una soluzione possono essere inclusi più progetti server di report. Quando si utilizzano più progetti, la gestione della distribuzione dei report può risultare più semplice, dal momento che è possibile distribuire progetti diversi tramite una diversa configurazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Pagine delle proprietà del progetto](../tools/project-property-pages-dialog-box.md)   
 [Gestione contenuto del server di report &#40;modalità nativa SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [Aggiornare i report](../install-windows/upgrade-reports.md)  
  
  
