---
title: Proprietà processo (Management Studio) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.jobproperties.f1
ms.assetid: 807ffd0e-9363-4f8f-9c36-c5d746ad19fd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fb1a989876126a57553a1ae833bcf847f9c005bc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65571123"
---
# <a name="job-properties-management-studio"></a>Proprietà processo (Management Studio)
  Usare la pagina **Proprietà processo** per visualizzare le informazioni su una sottoscrizione o su un report in corso prima di annullarlo.  
  
 Per aprire questa pagina, avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], connettersi a un server di report e aprire la cartella **Processi** . Fare clic con il pulsante destro del mouse su un processo in esecuzione, quindi scegliere **Proprietà**.  
  
> [!NOTE]  
>  Questa caratteristica non è supportata in [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services. Questa pagina non viene visualizzata quando è in esecuzione [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
## <a name="tasks"></a>Attività  
 Per visualizzare le informazioni su un processo, è prima necessario aggiornare la pagina per recuperare le informazioni sui processi attualmente in esecuzione nel server di report:  
  
1.  Aprire la cartella del server di report.  
  
2.  Fare clic con il pulsante destro del mouse su **Processi**, quindi scegliere **Aggiorna**.  
  
3.  Se un processo è presente nell'elenco, fare clic con il pulsante destro del mouse su di esso, quindi scegliere **Proprietà**.  
  
## <a name="options"></a>Opzioni  
 **ID processo**  
 GUID assegnato a un processo durante l'elaborazione. Il valore viene generato casualmente ogni volta che viene eseguito un report o una sottoscrizione.  
  
 **Stato processo**  
 I valori validi sono **Nuovo** e **In esecuzione**. All'avvio del processo, lo stato è sempre impostato come **Nuovo** . Dopo 60 secondi, lo stato viene modificato in **In esecuzione**. Per visualizzare la modifica, è necessario aggiornare la pagina.  
  
 **Tipo di processo**  
 I valori validi sono **Utente** e **Sistema**. Un processo utente è qualsiasi processo avviato da un singolo utente, inclusi l'esecuzione di un report su richiesta, la generazione manuale di uno snapshot della cronologia del report o la creazione manuale di uno snapshot dell'esecuzione del report. Anche una sottoscrizione standard in corso è un processo utente. Un processo di sistema è un processo avviato dal server di report. I processi di sistema includono l'elaborazione di report avviata da una pianificazione.  
  
 **Azione del processo**  
 Per i report, in questa colonna vengono indicati i processi di esecuzione del report in corso. Questo valore corrisponde sempre a **Rendering**.  
  
 **Descrizione del processo**  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per impostazione predefinita non fornisce descrizioni dei processi.  
  
 **Nome server**  
 Indica il nome del server di report che sta elaborando il processo. Se è stata configurata una distribuzione con scalabilità orizzontale, questo valore indica il server che sta elaborando il processo.  
  
 **Nome del report**  
 Indica il nome del report. Le sottoscrizioni sono identificate tramite le rispettive descrizioni.  
  
 **Percorso report**  
 Indica il percorso del report nella gerarchia di cartelle del server di report.  
  
 **Start Time**  
 Indica l'ora di inizio del processo.  
  
 **Nome utente**  
 Per i processi avviati da un utente, in questa colonna viene indicato il nome dell'utente. Per i processi di sistema, si tratta del nome del server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto del server di report in Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Eseguire la connessione a un server di report in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Gestire un processo in esecuzione](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
