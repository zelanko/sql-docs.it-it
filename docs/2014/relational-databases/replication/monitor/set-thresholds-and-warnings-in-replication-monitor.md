---
title: Impostare valori di soglia e avvisi in Monitoraggio replica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 13511f66d2636634daa11b8e6555bb1f5ccd335f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62667184"
---
# <a name="set-thresholds-and-warnings-in-replication-monitor"></a>Impostazione di valore soglia e avvisi in Monitoraggio replica
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] In Monitoraggio replica vengono visualizzate informazioni sullo stato delle pubblicazioni e delle sottoscrizioni. Per impostazione predefinita, in Monitoraggio replica vengono visualizzati avvisi solo per le sottoscrizioni non inizializzate, ma è possibile abilitarli anche per altre condizioni. È consigliabile abilitare gli avvisi per la topologia, in modo da poter essere informati tempestivamente sullo stato e sulle prestazioni.  
  
 Quando si attiva un avviso, si specifica una soglia. Quando tale soglia viene soddisfatta o superata, viene visualizzato un avviso, a meno che non sia necessario visualizzare un problema con una priorità più elevata. Oltre a visualizzare un avviso in Monitoraggio replica, il raggiungimento di un valore soglia può inoltre attivare un messaggio di avviso. È possibile abilitare avvisi per le seguenti condizioni:  
  
-   Imminente scadenza della sottoscrizione  
  
     Applicabile a tutti i tipi di replica. Se il valore soglia specificato viene raggiunto o superato, lo stato della sottoscrizione diventa **Scadenza imminente/Scaduta**.  
  
-   Superamento della latenza specificata (quantità di tempo trascorso tra l'esecuzione del commit di una transazione nel server di pubblicazione e l'esecuzione del commit della transazione corrispondente nel Sottoscrittore).  
  
     Si applica alla replica transazionale. Se la soglia specificata viene raggiunta o superata, lo stato della sottoscrizione diventa **Prestazioni critiche**.  
  
-   Superamento del tempo di sincronizzazione specificato.  
  
     Si applica alla replica di tipo merge. Se la soglia specificata viene raggiunta o superata, viene visualizzato lo stato **Merge con esecuzione prolungata**. È possibile specificare valore soglia differenti per le connessioni remote e le connessioni LAN.  
  
-   Impossibilità di elaborare il numero di righe specificato in un determinato intervallo di tempo.  
  
     Si applica alla replica di tipo merge. Se la soglia specificata viene raggiunta o superata, viene visualizzato lo stato **Prestazioni critiche**. È possibile specificare valore soglia differenti per le connessioni remote e le connessioni LAN.  
  
 Per altre informazioni sugli avvisi **Prestazioni critiche** e **Merge con esecuzione prolungata**, vedere [Monitoraggio delle prestazioni con Monitoraggio replica](monitor-performance-with-replication-monitor.md).  
  
 **Contenuto dell'articolo**  
  
-   [Impostare soglie e avvisi per una pubblicazione transazionale](#Transactional)  
  
-   [Impostare soglie e avvisi per una pubblicazione di tipo merge](#Merge)  
  
-   [Impostare soglie e avvisi per una pubblicazione snapshot](#Snapshot)  
  
##  <a name="Transactional"></a>Per impostare soglie e avvisi per una pubblicazione transazionale  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **avvisi** . Per visualizzare ulteriori informazioni sulle opzioni disponibili in questa scheda, **fare clic su** ? sulla barra dei menu.  
  
3.  Abilitare un avviso selezionando la casella di controllo appropriata tra **Avvisa se una sottoscrizione scade entro il valore soglia** e **Avvisa se la latenza supera il valore soglia**.  
  
4.  Impostare una soglia per gli avvisi nella colonna **Soglia** . Se, ad esempio, nel passaggio 3 è stata selezionata la casella di controllo **Avvisa se la latenza supera il valore soglia** , è possibile impostare una latenza di **60 secondi** nella colonna **Soglia** .  
  
5.  Fare clic su **Save Changes**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>Per configurare un avviso per una soglia  
  
1.  Fare clic su **Configura avvisi**.  
  
2.  Nella finestra di dialogo **Configura avvisi di replica** selezionare un avviso e quindi fare clic su **Configura**.  
  
     In questa finestra di dialogo vengono visualizzati gli avvisi per tutti i tipi di pubblicazione, inclusi quelli che non sono relativi al monitoraggio delle soglie. Per altre informazioni, vedere [Usare gli avvisi per gli eventi degli agenti di replica](../agents/use-alerts-for-replication-agent-events.md).  
  
3.  Impostare le ** \<** opzioni nella finestra di dialogo Proprietà avviso> alertName:  
  
    -   Nella pagina **Generale** fare clic su **Abilita**e specificare il database a cui si desidera applicare l'avviso.  
  
    -   Nella pagina **Risposta** specificare se si desidera inviare un messaggio di posta elettronica e/o eseguire un processo.  
  
    -   Nella pagina **Opzioni** personalizzare il testo della risposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Fare clic su **Close**.  
  
##  <a name="Merge"></a>Impostare soglie e avvisi per una pubblicazione di tipo merge  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **avvisi** . Per visualizzare ulteriori informazioni sulle opzioni **disponibili in questa scheda, fare clic** su? sulla barra dei menu.  
  
3.  Abilitare un avviso selezionando la casella di controllo appropriata tra  
  
    -   **Avvisa se una sottoscrizione scade entro la soglia**  
  
    -   **Avvisa se la durata del merge per le connessioni remote supera la soglia**  
  
    -   **Avvisa se la durata del merge per le connessioni LAN supera la soglia**  
  
    -   **Avvisa se le righe unite al secondo per le connessioni LAN sono inferiori alla soglia**  
  
    -   **Avvisa se le righe unite al secondo per le connessioni remote sono inferiori alla soglia**  
  
4.  Impostare i valore soglia per gli avvisi nella colonna **Soglia** . Ad esempio, se si seleziona **Avvisa se la durata del processo di merge per le connessioni remote supera il valore soglia** nel passaggio 3, è possibile selezionare un periodo di **10 minuti** nella colonna **Soglia** .  
  
5.  Fare clic su **Save Changes**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>Per configurare un avviso per una soglia  
  
1.  Fare clic su **Configura avvisi**.  
  
2.  Nella finestra di dialogo **Configura avvisi di replica** selezionare un avviso e quindi fare clic su **Configura**.  
  
     In questa finestra di dialogo vengono visualizzati gli avvisi per tutti i tipi di pubblicazione, inclusi quelli che non sono relativi al monitoraggio delle soglie.  
  
3.  Impostare le ** \<** opzioni nella finestra di dialogo Proprietà avviso> alertName:  
  
    -   Nella pagina **Generale** fare clic su **Abilita**e specificare il database a cui si desidera applicare l'avviso.  
  
    -   Nella pagina **Risposta** specificare se si desidera inviare un messaggio di posta elettronica e/o eseguire un processo.  
  
    -   Nella pagina **Opzioni** personalizzare il testo della risposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Fare clic su **Close**.  
  
##  <a name="Snapshot"></a>Impostare soglie e avvisi per una pubblicazione snapshot  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **avvisi** . Per visualizzare ulteriori informazioni sulle opzioni disponibili in questa scheda, **fare clic su** ? nel menu in alto.  
  
3.  Abilitare un avviso selezionando la casella di controllo **Avvisa se una sottoscrizione scade entro il valore soglia**.  
  
4.  Impostare una soglia per l'avviso nella colonna **Soglia** . È ad esempio possibile selezionare un valore di **70%** nella colonna **Soglia** .  
  
5.  Fare clic su **Save Changes**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>Per configurare un avviso per una soglia  
  
1.  Fare clic su **Configura avvisi**.  
  
2.  Nella finestra di dialogo **Configura avvisi di replica** selezionare un avviso e quindi fare clic su **Configura**.  
  
     In questa finestra di dialogo vengono visualizzati gli avvisi per tutti i tipi di pubblicazione, inclusi quelli che non sono relativi al monitoraggio delle soglie. Per altre informazioni, vedere [Usare gli avvisi per gli eventi degli agenti di replica](../agents/use-alerts-for-replication-agent-events.md).  
  
3.  Impostare le ** \<** opzioni nella finestra di dialogo Proprietà avviso> alertName:  
  
    -   Nella pagina **Generale** fare clic su **Abilita**e specificare il database a cui si desidera applicare l'avviso.  
  
    -   Nella pagina **Risposta** specificare se si desidera inviare un messaggio di posta elettronica e/o eseguire un processo.  
  
    -   Nella pagina **Opzioni** personalizzare il testo della risposta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Fare clic su **Close**.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio della replica](../monitoring-replication.md)  
  
  
