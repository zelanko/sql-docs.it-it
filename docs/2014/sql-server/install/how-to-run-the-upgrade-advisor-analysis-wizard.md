---
title: "Procedura: Eseguire l'analisi guidata di preparazione aggiornamento | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 49c8cd84ada68d4ac00b13567528abff72d13847
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207650"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>Procedura: Eseguire l'analisi guidata di preparazione aggiornamento
  È possibile avviare l'Analisi guidata di Preparazione aggiornamento dalla pagina iniziale di Preparazione aggiornamento. In questo argomento viene descritto come eseguire l'Analisi guidata di Preparazione aggiornamento.  
  
> [!IMPORTANT]
>  Quando si esegue l'Analisi guidata di Preparazione aggiornamento, i report vengono salvati nella cartella di report predefinita. Tuttavia, nel visualizzatore di report vengono visualizzati solo gli ultimi cinque report salvati. Il percorso predefinito per i report è documenti\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Advisor\110\Reports esegue l'aggiornamento.  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>Per eseguire l'Analisi guidata di Preparazione aggiornamento  
  
1.  Nella pagina iniziale di preparazione aggiornamento, fare clic su **avviare Analisi guidata Preparazione aggiornamento**.  
  
2.  Nel  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componenti** pagina, immettere il nome del server da analizzare nel **nome del Server** casella e quindi fare clic su **rileva**. Utilizzare le linee guida seguenti per il nome del server:  
  
    -   Per analizzare istanze non cluster, immettere il nome del computer.  
  
    -   Per analizzare istanze cluster, immettere il nome [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] virtuale.  
  
    -   Per analizzare i componenti non cluster installati in un nodo di un cluster, immettere il nome del nodo.  
  
    > [!WARNING]  
    >  Preparazione aggiornamento non supporta la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non sia impostata per utilizzare la porta standard (1433) per le connessioni client. Se si desidera connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non utilizza la porta standard (1433), creare un alias utilizzando l'indirizzo IP e la porta. Per altre informazioni sulla configurazione dei protocolli client e la creazione di un alias per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanze, vedere [Configure Client Protocols](../../database-engine/configure-windows/configure-client-protocols.md).  
    >   
    >  Se non hai [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installato nel computer in cui si esegue Preparazione aggiornamento, fare clic su **avviare**, quindi eseguire `cliconfg`. Verrà visualizzata la  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilità di rete Client** nella finestra di dialogo. Usare la **Alias** pressione di tab per creare l'alias.  
  
3.  Esaminare l'elenco dei componenti rilevati, se necessario, modificare le selezioni e quindi fare clic su **successivo**.  
  
4.  Nel **parametri di connessione** pagina, selezionare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si desidera analizzare, selezionare il metodo di autenticazione e, se necessario, immettere le informazioni di nome e una password utente e quindi fare clic su **successivo**.  
  
     Il nome dell'istanza predefinita è MSSQLSERVER.  
  
5.  Per i componenti selezionati, immettere le informazioni richieste. Per altre informazioni sulle singole finestre di dialogo, vedere [esegue l'aggiornamento dell'interfaccia utente di Advisor](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
6.  Nel **conferma impostazione di preparazione aggiornamento** pagina, esaminare le informazioni immesse. È possibile selezionare **inviare report a [!INCLUDE[msCoName](../../includes/msconame-md.md)]**  se si desidera inviare il report di aggiornamento. È inoltre possibile consultare l'informativa sulla privacy.  
  
7.  Fare clic su **eseguiti** per analizzare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
8.  Al termine dell'analisi, fare clic su **avvia Report** per visualizzare i problemi di aggiornamento rilevati.  
  
## <a name="see-also"></a>Vedere anche  
 [Come si fa: Avvio di preparazione aggiornamento](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Esecuzione di preparazione aggiornamento a &#40;interfaccia utente&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
