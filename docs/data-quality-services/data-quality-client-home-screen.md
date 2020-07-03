---
title: Schermata iniziale del client Data Quality
ms.date: 02/29/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.clienthome.f1
ms.assetid: 7c6ec469-bc7d-4d19-8e21-11dcf8ade108
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 4b1a25fc4bee5c66838c7e29f7c34dc67a572b79
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899112"
---
# <a name="data-quality-client-home-screen"></a>Schermata iniziale del client Data Quality

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  Questa schermata consente di accedere alle interfacce utente per ciascuno dei tre gruppi principali di attività [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS): gestione della Knowledge Base, progetti Data Quality e amministrazione.  
  
## <a name="options"></a>Opzioni  
  
### <a name="knowledge-base-management"></a>Gestione Knowledge Base  
 Una Knowledge Base DQS è un repository di metadati utilizzati da DQS per migliorare la qualità dei dati. Questi metadati vengono creati sia dalla piattaforma DQS in un processo computerizzato di individuazione delle informazioni che dall'amministratore dei dati in un processo interattivo di gestione del dominio.  
  
 **Nuova Knowledge Base**  
 Consente di avviare il processo di creazione di una Knowledge Base da zero o in base ai metadati di una Knowledge Base esistente. Questo comando consente di aprire una pagina nella quale è possibile identificare la Knowledge Base, basarla su una Knowledge Base esistente, selezionare l'attività desiderata relativa alla Knowledge Base, quindi creare la Knowledge Base.  
  
 **Apri Knowledge Base**  
 Consente di aprire una Knowledge Base per gestirne i domini, eseguire l'individuazione delle informazioni o creare criteri di corrispondenza. Se si fa clic sul pulsante **Apri Knowledge Base** , viene visualizzata la pagina **Apri Knowledge Base** che contiene un elenco di Knowledge Base esistenti con le relative proprietà, lo stato corrente e i dettagli dei domini. Selezionare una Knowledge Base e aprirla da **Apri Knowledge Base**.  
  
 **Knowledge Base recente**  
 Dall'elenco visualizzato, aprire una Knowledge Base già creata. Se non è bloccata, fare clic sulla freccia destra, quindi selezionare l'attività nella quale avviare la Knowledge Base (Gestione dominio, Individuazione informazioni o Criteri di corrispondenza).  
  
 È possibile aprire una Knowledge Base bloccata e modificarla solo se si è gli autori del blocco. In tal caso, la Knowledge Base verrà aperta nello stato in cui era al momento della chiusura, indicato in parentesi. Se una Knowledge Base è bloccata e non si è gli autori del blocco, è possibile aprirla solo in sola lettura.  
  
### <a name="data-quality-projects"></a>Progetti Data Quality  
 Un progetto Data Quality è il processo tramite cui viene eseguita la pulizia o la corrispondenza dei dati in DQS, sia attraverso un'attività di correzione dei dati assistita da computer che attraverso la pulizia interattiva dei dati.  
  
 **Nuovo progetto Data Quality**  
 Consente di avviare il processo di creazione di un nuovo progetto. Questo comando consente di aprire una pagina nella quale è possibile identificare il progetto, associarlo a una Knowledge Base, visualizzare i dettagli della Knowledge Base, selezionare l'attività di progetto desiderata, quindi creare il progetto.  
  
 **Apri progetto Data Quality**  
 Consente di aprire un progetto per effettuare la pulizia o la corrispondenza dei dati. Se si fa clic sul pulsante **Apri progetto Data Quality** , viene visualizzata la pagina **Apri progetto Data Quality** che contiene un elenco di progetti esistenti con le relative proprietà, lo stato corrente, la Knowledge Base, i dettagli dei domini e le regole dei criteri di corrispondenza. Selezionare un progetto e aprirlo da **Apri progetto Data Quality**.  
  
 **Progetto Data Quality recente**  
 Dall'elenco visualizzato, selezionare un progetto già creato. È possibile aprire un progetto bloccato solo se si è gli autori del blocco. In tal caso, il progetto verrà aperto nello stato in cui era al momento della chiusura, indicato in parentesi. Se il progetto è stato completato, verrà aperto nel passaggio Esporta dell'attività.  
  
### <a name="administration"></a>Amministrazione  
 L'amministrazione DQS consente di monitorare, configurare e gestire DQS.  
  
 **Monitoraggio attività**  
 Consente di visualizzare lo stato di tutte le attività (sia correnti che passate) correlate al [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]connesso. I tipi di attività monitorati includono Gestione informazioni, Progetto Data Quality e la correzione dei dati basata su SSIS.  
  
 **Configuration**  
 Visualizzare le proprietà di configurazione per gli account del servizio dati di riferimento (sia tramite Azure Marketplace che direttamente ai servizi dati di riferimento), le impostazioni generali (pulizia interattiva, corrispondenza e profiling) e le impostazioni di gravità del log.  
  
## <a name="see-also"></a>Vedere anche  
 [Knowledge base e domini DQS](../data-quality-services/dqs-knowledge-bases-and-domains.md)   
 [Progetti Data Quality &#40;&#41;DQS](../data-quality-services/data-quality-projects-dqs.md)   
 [amministrazione dqs](../data-quality-services/dqs-administration.md)  
  
  
