---
title: Connettersi a un Server di Report in modalità nativa | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.connectiondialog.F1
helpviewer_keywords:
- report servers [Reporting Services], configuring
ms.assetid: 8b9ea8d3-827c-4011-9e02-be2eac3bb364
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 95062797cdfe8f2ab4bc2f3b8b8bb2735d2d0dcf
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52395824"
---
# <a name="connect-to-a-native-mode-report-server"></a>Connettersi a un server di report in modalità nativa
  Utilizzare questa finestra di dialogo per connettersi a un'istanza locale o remota del server di report [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versione successiva [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Non è possibile utilizzare questo strumento per connettersi a versioni precedenti di server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . È possibile connettersi a una singola istanza per volta.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
>  Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è utilizzato per configurare e amministrare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint. Utilizzare Amministrazione centrale SharePoint e script di PowerShell per configurare un server di report in modalità SharePoint. Per altre informazioni, vedere [Installare la modalità SharePoint di Reporting Services per SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
> [!TIP]  
>  Il[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager (RSConfigTool.exe) viene installato con un livello di privilegio "highestAvailable". Questo comportamento si verifica per motivi strutturali. Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] richiede la comunicazione con le API di WMI per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Una parte della comunicazione di WMI per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] richiede un livello superiore o privilegi amministrativi.  
  
-   Per connettersi a un'istanza locale del server di report, utilizzare i valori predefiniti e fare clic su **Connetti**. Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornisce il nome del server locale e rileva l'istanza predefinita. Nella maggior parte dei casi, è possibile fare clic su **Connetti** senza dovere modificare i valori. Se sono state installate più istanze, è necessario selezionare quella che si desidera utilizzare.  
  
-   Per connettersi a un'istanza remota del server di report, digitare il nome del server, fare clic su **Trova**, selezionare l'istanza, quindi fare clic su **Connetti**.  
  
 Per aprire questa finestra di dialogo, avviare Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La finestra di dialogo verrà visualizzata non appena si avvia lo strumento. Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opzioni  
 **Nome server**  
 Consente di immettere il nome di rete del computer in cui è installato [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versione successiva [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Digitare solo il nome del computer senza includere barre o un prefisso.  
  
 **trovare**  
 Consente di trovare il computer specificato in **Nome server**.  
  
 **Istanza del Server di report**  
 Consente di selezionare l'istanza a cui connettersi se sono installate più istanze del server di report. Solo le istanze valide saranno disponibili per la selezione. Se si eseguono versioni precedenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità affiancata con un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tali istanze non saranno incluse nell'elenco.  
  
 **Connect**  
 Consente di connettersi al server e all'istanza specificati.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
