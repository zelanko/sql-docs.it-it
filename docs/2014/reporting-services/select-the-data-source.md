---
title: Selezionare l'origine dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptwizard.selectdatasource.f1
ms.assetid: cdd84ad8-7c6a-41ac-bf51-1b0973434829
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6dab6158ba2d0854868bf60f2a73efce594b2cc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101435"
---
# <a name="select-the-data-source"></a>Selezione origine dati
  Utilizzare questa pagina della Creazione guidata report per definire un'origine dati per il report.  
  
## <a name="options"></a>Opzioni  
 **Origine dati condivisa**  
 Selezionare **Origine dati condivisa** per usare un'origine dei dati condivisa in cui siano già disponibili le informazioni sulla connessione all'origine dei dati che si desidera usare. Nell'elenco sono presenti tutte le origini dei dati incluse nel progetto.  
  
 **Nuova origine dati**  
 Selezionare **Nuova origine dati** per definire una nuova origine dei dati. Le informazioni dell'origine dati verranno utilizzate solo per il report corrente.  
  
 **Name**  
 Consente di digitare un nome per la connessione all'origine dati. Tale nome deve essere univoco all'interno del report.  
  
 **Tipo**  
 Consente di selezionare il tipo di origine dati usata. Se, ad esempio, si utilizza un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , selezionare [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Stringa di connessione**  
 Consente di digitare una stringa di connessione per l'origine dati. Per altre informazioni sulle stringhe di connessione, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 Fare clic su **Modifica** per specificare il server dell'origine dati nella finestra di dialogo **Proprietà connessione** . È possibile specificare un'origine dati remota o locale.  
  
 Fare clic su **Credenziali** per specificare le credenziali per il database. Le credenziali specificate devono essere sufficienti per connettersi all'origine dei dati per la progettazione dei report. Quando il report è distribuito in un server di report, le credenziali per il database devono poter essere utilizzate da tutti gli utenti del report. Se, ad esempio, si desidera che tutti gli utenti del report usino le proprie credenziali per connettersi all'origine dati, selezionare **Usa autenticazione di Windows (sicurezza integrata)** . Le credenziali specificate devono essere valide per l'origine dati. Se, pertanto, si seleziona l'autenticazione di Windows, accertarsi che l'origine dati accetti connessioni da tutti gli account utente che eseguiranno il report. Le credenziali per il database possono essere gestite separatamente dal report. Per altre informazioni, vedere [Gestire origini dati dei report](report-data/manage-report-data-sources.md).  
  
 **Imposta come origine dati condivisa**  
 Selezionare questa opzione per archiviare l'origine dati nel progetto, anziché nel report, come origine dati condivisa. In questo modo, potrà essere utilizzata come origine dati per altri report nel progetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni dati o origini dati incorporate e condivise &#40;Generatore report e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Reporting Services Report Server](../../2014/reporting-services/reporting-services-report-server.md)   
 [RSReportDesigner - file di configurazione](report-server/rsreportdesigner-configuration-file.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Guida della Creazione guidata report](../../2014/reporting-services/report-wizard-help.md)  
  
  
