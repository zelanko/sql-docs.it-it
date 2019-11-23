---
title: Connettersi a un server di report in modalità nativa | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.connectiondialog.F1
helpviewer_keywords:
- report servers [Reporting Services], configuring
ms.assetid: 8b9ea8d3-827c-4011-9e02-be2eac3bb364
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5bf32c8427679b342bee89d6541b051beed2e8ce
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952295"
---
# <a name="connect-to-a-native-mode-report-server"></a>Connettersi a un server di report in modalità nativa
  Utilizzare questa finestra di dialogo per connettersi a un'istanza locale o remota del server di report [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versione successiva [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Non è possibile utilizzare questo strumento per connettersi a versioni precedenti di server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . È possibile connettersi a una singola istanza per volta.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
>  Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è utilizzato per configurare e amministrare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint. Utilizzare Amministrazione centrale SharePoint e script di PowerShell per configurare un server di report in modalità SharePoint. Per altre informazioni, vedere [Installare la modalità SharePoint di Reporting Services per SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
> [!TIP]  
>  Il[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager (RSConfigTool. exe) viene installato con un livello di privilegio "highestAvailable". Questo comportamento si verifica per motivi strutturali. Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] richiede la comunicazione con le API di WMI per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Una parte della comunicazione di WMI per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] richiede un livello superiore o privilegi amministrativi.  
  
-   Per connettersi a un'istanza locale del server di report, utilizzare i valori predefiniti e fare clic su **Connetti**. Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornisce il nome del server locale e rileva l'istanza predefinita. Nella maggior parte dei casi, è possibile fare clic su **Connetti** senza dovere modificare i valori. Se sono state installate più istanze, è necessario selezionare quella che si desidera utilizzare.  
  
-   Per connettersi a un'istanza remota del server di report, digitare il nome del server, fare clic su **Trova**, selezionare l'istanza, quindi fare clic su **Connetti**.  
  
 Per aprire questa finestra di dialogo, avviare Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La finestra di dialogo verrà visualizzata non appena si avvia lo strumento. Per altre informazioni, vedere [Reporting Services Configuration Manager &#40;Native Mode&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opzioni  
 **Server Name**  
 Consente di immettere il nome di rete del computer in cui è installato [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versione successiva [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Digitare solo il nome del computer senza includere barre o un prefisso.  
  
 **Trovare**  
 Consente di trovare il computer specificato in **Nome server**.  
  
 **Istanza del server di report**  
 Consente di selezionare l'istanza a cui connettersi se sono installate più istanze del server di report. Solo le istanze valide saranno disponibili per la selezione. Se si eseguono versioni precedenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità affiancata con un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tali istanze non saranno incluse nell'elenco.  
  
 **Connetti**  
 Consente di connettersi al server e all'istanza specificati.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
