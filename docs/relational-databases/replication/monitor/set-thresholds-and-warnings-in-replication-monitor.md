---
title: Impostare valori di soglia e avvisi (Monitoraggio replica)
description: Informazioni su come abilitare avvisi per diverse condizioni che possono verificarsi con la replica tramite Monitoraggio replica in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- Merge Agent, thresholds and warnings
- Distribution Agent, thresholds and warnings
- thresholds [SQL Server replication]
- Replication Monitor, thresholds and warnings
- monitoring performance [SQL Server replication], thresholds and warnings
ms.assetid: 3a409c2c-b77e-4001-b81a-1dcd918618ec
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: bf3d9ba88f433619a79c9f4453823e81589b4ee3
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322273"
---
# <a name="set-thresholds-and-warnings-in-replication-monitor"></a>Impostazione di valore soglia e avvisi in Monitoraggio replica
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Monitoraggio replica per [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] visualizza informazioni sullo stato delle pubblicazioni e delle sottoscrizioni. Per impostazione predefinita, in Monitoraggio replica vengono visualizzati avvisi solo per le sottoscrizioni non inizializzate, ma è possibile abilitarli anche per altre condizioni. È consigliabile abilitare gli avvisi per la topologia, in modo da poter essere informati tempestivamente sullo stato e sulle prestazioni.  
  
 Quando si attiva un avviso, si specifica una soglia. Quando tale soglia viene soddisfatta o superata, viene visualizzato un avviso, a meno che non sia necessario visualizzare un problema con una priorità più elevata. Oltre a visualizzare un avviso in Monitoraggio replica, il raggiungimento di un valore soglia può inoltre attivare un messaggio di avviso. È possibile abilitare avvisi per le seguenti condizioni:  
  
-   Imminente scadenza della sottoscrizione  
  
     Applicabile a tutti i tipi di replica. Se il valore soglia specificato viene raggiunto o superato, lo stato della sottoscrizione diventa **Scadenza imminente/Scaduta**.  
  
-   Superamento della latenza specificata (quantità di tempo trascorso tra l'esecuzione del commit di una transazione nel server di pubblicazione e l'esecuzione del commit della transazione corrispondente nel Sottoscrittore).  
  
     Si applica alla replica transazionale. Se la soglia specificata viene raggiunta o superata, lo stato della sottoscrizione diventa **Prestazioni critiche**.  
  
-   Superamento del tempo di sincronizzazione specificato.  
  
     Si applica alla replica di tipo merge. Se la soglia specificata viene raggiunta o superata, viene visualizzato lo stato **Merge con esecuzione prolungata**. È possibile specificare valore soglia differenti per le connessioni remote e le connessioni LAN.  
  
-   Impossibilità di elaborare il numero di righe specificato in un determinato intervallo di tempo.  
  
     Si applica alla replica di tipo merge. Se la soglia specificata viene raggiunta o superata, viene visualizzato lo stato **Prestazioni critiche**. È possibile specificare valore soglia differenti per le connessioni remote e le connessioni LAN.  
  
 Per altre informazioni sugli avvisi **Prestazioni critiche** e **Merge con esecuzione prolungata**, vedere [Monitoraggio delle prestazioni con Monitoraggio replica](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **Contenuto dell'articolo**  
  
-   [Impostare soglie e avvisi per una pubblicazione transazionale](#Transactional)  
  
-   [Impostare valore soglia e avvisi per una pubblicazione di tipo merge](#Merge)  
  
-   [Impostare valore soglia e avvisi per una pubblicazione di snapshot](#Snapshot)  
  
##  <a name="Transactional"></a> Per impostare soglie e avvisi per una pubblicazione transazionale  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Avvisi** . Per visualizzare ulteriori informazioni sulle opzioni di questa scheda, fare clic su **?** sulla barra dei menu.  
  
3.  Abilitare un avviso selezionando la casella di controllo appropriata tra **Avvisa se una sottoscrizione scade entro il valore soglia** e **Avvisa se la latenza supera il valore soglia**.  
  
4.  Impostare una soglia per gli avvisi nella colonna **Soglia** . Se, ad esempio, nel passaggio 3 è stata selezionata la casella di controllo **Avvisa se la latenza supera il valore soglia** , è possibile impostare una latenza di **60 secondi** nella colonna **Soglia** .  
  
5.  Fare clic su **Salva modifiche**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>Per configurare un avviso per una soglia  
  
1.  Fare clic su **Configura avvisi**.  
  
2.  Nella finestra di dialogo **Configura avvisi di replica** selezionare un avviso e quindi fare clic su **Configura**.  
  
     In questa finestra di dialogo vengono visualizzati gli avvisi per tutti i tipi di pubblicazione, inclusi quelli che non sono relativi al monitoraggio delle soglie. Per altre informazioni, vedere [Usare gli avvisi per gli eventi degli agenti di replica](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
3.  Impostare le opzioni nella finestra di dialogo **Proprietà dell'avviso \<NomeAvviso>** :  
  
    -   Nella pagina **Generale** fare clic su **Abilita**e specificare il database a cui si desidera applicare l'avviso.  
  
    -   Nella pagina **Risposta** specificare se si desidera inviare un messaggio di posta elettronica e/o eseguire un processo.  
  
    -   Nella pagina **Opzioni** personalizzare il testo della risposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Fare clic su **Close**.  
  
##  <a name="Merge"></a> Impostare valore soglia e avvisi per una pubblicazione di tipo merge  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Avvisi** . Per visualizzare altre informazioni relative alle opzioni della scheda, fare clic su **?** sulla barra dei menu.  
  
3.  Abilitare un avviso selezionando la casella di controllo appropriata tra  
  
    -   **Avvisa se una sottoscrizione scade entro il valore soglia**  
  
    -   **Avvisa se la durata del processo di merge per le connessioni remote supera il valore soglia**  
  
    -   **Avvisa se la durata del processo di merge per le connessioni LAN supera il valore soglia**  
  
    -   **Avvisa se il numero di righe al secondo di cui è stato eseguito il merge per le connessioni LAN è minore del valore soglia**  
  
    -   **Avvisa se il numero di righe al secondo di cui è stato eseguito il merge per le connessioni remote è minore del valore soglia**  
  
4.  Impostare i valore soglia per gli avvisi nella colonna **Soglia** . Ad esempio, se si seleziona **Avvisa se la durata del processo di merge per le connessioni remote supera il valore soglia** nel passaggio 3, è possibile selezionare un periodo di **10 minuti** nella colonna **Soglia** .  
  
5.  Fare clic su **Salva modifiche**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>Per configurare un avviso per una soglia  
  
1.  Fare clic su **Configura avvisi**.  
  
2.  Nella finestra di dialogo **Configura avvisi di replica** selezionare un avviso e quindi fare clic su **Configura**.  
  
     In questa finestra di dialogo vengono visualizzati gli avvisi per tutti i tipi di pubblicazione, inclusi quelli che non sono relativi al monitoraggio delle soglie.  
  
3.  Impostare le opzioni nella finestra di dialogo **Proprietà dell'avviso \<NomeAvviso>** :  
  
    -   Nella pagina **Generale** fare clic su **Abilita**e specificare il database a cui si desidera applicare l'avviso.  
  
    -   Nella pagina **Risposta** specificare se si desidera inviare un messaggio di posta elettronica e/o eseguire un processo.  
  
    -   Nella pagina **Opzioni** personalizzare il testo della risposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Fare clic su **Close**.  
  
##  <a name="Snapshot"></a> Impostare valore soglia e avvisi per una pubblicazione di snapshot  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Avvisi** . Per visualizzare ulteriori informazioni sulle opzioni di questa scheda, scegliere **?** dal menu disponibile nella parte superiore.  
  
3.  Abilitare un avviso selezionando la casella di controllo **Avvisa se una sottoscrizione scade entro il valore soglia**.  
  
4.  Impostare una soglia per l'avviso nella colonna **Soglia** . È ad esempio possibile selezionare un valore di **70%** nella colonna **Soglia** .  
  
5.  Fare clic su **Salva modifiche**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>Per configurare un avviso per una soglia  
  
1.  Fare clic su **Configura avvisi**.  
  
2.  Nella finestra di dialogo **Configura avvisi di replica** selezionare un avviso e quindi fare clic su **Configura**.  
  
     In questa finestra di dialogo vengono visualizzati gli avvisi per tutti i tipi di pubblicazione, inclusi quelli che non sono relativi al monitoraggio delle soglie. Per altre informazioni, vedere [Usare gli avvisi per gli eventi degli agenti di replica](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
3.  Impostare le opzioni nella finestra di dialogo **Proprietà dell'avviso \<NomeAvviso>** :  
  
    -   Nella pagina **Generale** fare clic su **Abilita**e specificare il database a cui si desidera applicare l'avviso.  
  
    -   Nella pagina **Risposta** specificare se si desidera inviare un messaggio di posta elettronica e/o eseguire un processo.  
  
    -   Nella pagina **Opzioni** personalizzare il testo della risposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Fare clic su **Close**.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio della replica](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
