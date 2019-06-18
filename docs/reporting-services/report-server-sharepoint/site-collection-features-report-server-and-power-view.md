---
title: Attivare le funzionalità di integrazione del server di report e di Power View in SharePoint | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: dce33b0f267dadd8454378fccb72112970553a96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580509"
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>Attivare le funzionalità di integrazione del server di report e di Power View in SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Le funzionalità di raccolta siti di Reporting Services vengono attivate per impostazione predefinita dopo l'installazione del componente aggiuntivo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] per prodotti SharePoint. In alcune situazioni è necessario attivare le funzionalità manualmente.  

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

 Se si installa il componente aggiuntivo Reporting Services per prodotti SharePoint 2010 dopo l'installazione del prodotto SharePoint, la funzionalità di integrazione del server di report e la funzionalità di integrazione di Power View verranno attivate solo per le raccolte siti radice. Per le altre raccolte di siti è necessario attivare le funzionalità manualmente. Ad esempio, in presenza di una raccolta siti **https://[nome server]/sites/[nome raccolta siti]** sarà necessario attivare manualmente le funzionalità di raccolta siti di Reporting Services.  
  
 Se non è presente alcuna raccolta siti radice, il componente aggiuntivo Reporting Services registrerà un messaggio simile al seguente.  
  
 "L'applicazione Web SharePoint 80 non dispone della raccolta siti radice"  
  
 Il messaggio è disponibile nel log di installazione del componente aggiuntivo con il nome "RS_SP_#.log" dove # è un numero incrementale. Il file di log si trova nella cartella Temp dell'utente corrente, ad esempio C:\Utenti\\[nome utente]\AppData\Local\Temp. Per altre informazioni sulle opzioni di registrazione con il componente aggiuntivo, vedere [Installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>Attivare le funzionalità di raccolta siti per l'integrazione del server di report e di Power View
  
1.  Accedere con il browser al sito in cui si intende attivare le funzionalità di Reporting Services.  
  
2.  Fare clic su **Azioni sito**.  
  
3.  Fare clic su **Impostazioni sito**.  
  
4.  Fare clic su **Funzionalità raccolta siti** nel gruppo Amministrazione raccolta siti  
  
5.  Individuare **Funzionalità di integrazione Server report** o **Funzionalità di integrazione Power View** nell'elenco.  
  
6.  Fare clic su **Attiva**.  
  
 Per disattivare le funzionalità, è possibile utilizzare la stessa procedura facendo clic su **Disattiva** anziché su **Attiva**.  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>Attivare o disattivare la funzionalità di raccolta siti dell'amministrazione centrale di Reporting Services
  
1.  Aprire il browser alla pagina Amministrazione centrale SharePoint.  
  
2.  Fare clic su **Azioni sito**.  
  
3.  Fare clic su **Impostazioni sito**.  
  
4.  Fare clic su **Funzionalità raccolta siti** nel gruppo Amministrazione raccolta siti  
  
5.  Individuare **Funzionalità Amministrazione centrale del server di report** nell'elenco.  
  
6.  Fare clic su **Attiva**.  
  
 Per disattivare la funzionalità, è possibile utilizzare la stessa procedura facendo tuttavia clic su **Disattiva** anziché su **Attiva.**  
  
## <a name="next-steps"></a>Passaggi successivi

Dopo aver attivato la funzionalità, è possibile continuare con l'integrazione del server.

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
