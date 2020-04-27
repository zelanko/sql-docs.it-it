---
title: Proprietà server (pagina sicurezza) - Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a49f56c4e898b0189ce0f8bf5008873e13dc6223
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099563"
---
# <a name="server-properties-security-page---reporting-services"></a>Proprietà server (pagina sicurezza) - Reporting Services
  Questa pagina consente di disattivare le caratteristiche che potrebbero compromettere un server di report. La disattivazione di queste caratteristiche comporta l'impostazione di determinati limiti, ma consente di migliorare la sicurezza globale del server di report riducendo i rischi di minacce specifiche.  
  
 Per aprire questa pagina, avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], connettersi a un'istanza del server di report, fare clic con il pulsante destro del mouse sul nome del server di report e scegliere **Proprietà**. Fare clic su **sicurezza** per aprire la pagina.  
  
## <a name="options"></a>Opzioni  
 **Attiva la sicurezza integrata di Windows per le origini dati dei report**  
 Consente di specificare se è possibile stabilire una connessione all'origine dati di un report utilizzando il token di sicurezza di Windows dell'utente che ha richiesto il report.  
  
 Se si disattiva questa caratteristica, la sicurezza integrata di Windows non sarà disponibile nelle pagine delle proprietà dell'origine dati del report. Se le origini dati del report sono configurate per la sicurezza integrata di Windows e successivamente si disattiva questa caratteristica, nel server di report vengono immediatamente aggiornate tutte le proprietà di connessione all'origine dati in modo che vengano richieste le credenziali.  
  
 **Consenti reporting ad hoc**  
 Consente di specificare se gli utenti possono eseguire query ad hoc da un report di Generatore report, nel caso in cui i nuovi report vengano generati automaticamente quando un utente fa clic su dati di interesse.  
  
 L'impostazione di questa opzione determina se il valore della proprietà `EnableLoadReportDefinition` nel server di report è impostato su `True` o su `False`. Se si deseleziona questa opzione, la proprietà viene impostata su `False` e nel server di report non verranno generati report click-through creati durante l'esplorazione dei dati. Tutte le chiamate al metodo `LoadReportDefinition` verranno bloccate.  
  
 La disattivazione di questa opzione consente di attenuare i rischi di attacchi Denial of Service condotti da utenti malintenzionati tramite overload del server di report con richieste `LoadReportDefinition`.  
  
## <a name="see-also"></a>Vedi anche  
 [Impostazione delle proprietà del server di report &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Connettersi a un server di report in Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Specificare le credenziali e le informazioni di connessione per le origini dati del report] (.. /report-data/Specify-Credential-and-Connection-Information-for-report-data-sources.MD [del server di report nella Guida sensibile al contesto Management Studio](report-server-in-management-studio-f1-help.md)  
  
  
