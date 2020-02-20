---
title: Proprietà server (pagina sicurezza) - Reporting Services | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
author: maggiesMSFT
ms.author: maggies
ms.date: 06/10/2016
ms.openlocfilehash: 0e29dcf7681d105f92b3bf187c38ebe764d2449e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65571319"
---
# <a name="server-properties-security-page---reporting-services"></a>Proprietà server (pagina sicurezza) - Reporting Services

  Usare questa pagina di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] per disattivare le caratteristiche che possono compromettere un server di report. La disattivazione di queste caratteristiche comporta l'impostazione di determinati limiti, ma consente di migliorare la sicurezza globale del server di report riducendo i rischi di minacce specifiche.  
  
 Per aprire la pagina:
 1) Avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Connettersi a un'istanza del server di report.
 3) Fare clic con il pulsante destro del mouse sul nome del server di report, quindi scegliere **Proprietà**.
 4) Fare clic su **sicurezza** per aprire la pagina.  
  
## <a name="options"></a>Opzioni

### <a name="enable-windows-integrated-security-for-report-data-sources"></a>Attiva la sicurezza integrata di Windows per le origini dati dei report

 Consente di specificare se una connessione all'origine dati di un report usa il token di sicurezza di Windows dell'utente che ha richiesto il report.  
  
 Se si disattiva questa caratteristica, la sicurezza integrata di Windows non è disponibile nelle pagine delle proprietà dell'origine dati del report. Se le origini dati del report sono configurate per la sicurezza integrata di Windows e successivamente si disattiva questa caratteristica, nel server di report vengono aggiornate immediatamente tutte le proprietà di connessione all'origine dati, in modo che vengano richieste le credenziali.  
  
### <a name="enable-ad-hoc-reporting"></a>Consenti reporting ad hoc

 Consente di specificare se gli utenti possono eseguire query ad hoc da un report di Generatore report, nel caso in cui i nuovi report vengano generati automaticamente quando un utente fa clic su dati di interesse.  
  
 L'impostazione di questa opzione determina se il valore della proprietà **EnableLoadReportDefinition** nel server di report è impostato su **True** o su **False**. Se si deseleziona questa opzione la proprietà viene impostata su **False** e nel server di report non vengono generati i report click-through creati durante l'esplorazione dei dati. Qualsiasi chiamata al metodo **LoadReportDefinition** viene bloccata.  
  
 La disattivazione di questa opzione consente di attenuare i rischi di attacchi Denial of Service condotti da utenti malintenzionati tramite overload del server di report con richieste **LoadReportDefinition** .  
  
## <a name="see-also"></a>Vedere anche

 [Impostare le proprietà di un server di report &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md) [Eseguire la connessione a un server di report in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md) [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) [Guida sensibile al contesto del server di report in Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)
