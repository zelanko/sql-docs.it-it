---
title: "Procedura: Eseguire l'analisi guidata di preparazione aggiornamento | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8481a6d3e6d7e07753cecb2ce2ff91ea626a4dfe
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811103"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>Procedura: Eseguire l'analisi guidata di Gestione spazio aggiornamenti
  È possibile avviare l'Analisi guidata di Preparazione aggiornamento dalla pagina iniziale di Preparazione aggiornamento. In questo argomento viene descritto come eseguire l'Analisi guidata di Preparazione aggiornamento.  
  
> [!IMPORTANT]
>  Quando si esegue l'Analisi guidata di Preparazione aggiornamento, i report vengono salvati nella cartella di report predefinita. Tuttavia, nel visualizzatore di report vengono visualizzati solo gli ultimi cinque report salvati. Il percorso predefinito per i report è My Documents\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] upgrade Advisor\110\Reports.  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>Per eseguire l'Analisi guidata di Preparazione aggiornamento  
  
1.  Nella pagina iniziale di preparazione aggiornamento fare clic su **Avvia l'analisi guidata di preparazione aggiornamento**.  
  
2.  Nella pagina **componentiimmettereilnomedelserverdaanalizzarenellacasellanomeserver,quindifare[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** clic su rileva. Utilizzare le linee guida seguenti per il nome del server:  
  
    -   Per analizzare le istanze non cluster, immettere il nome del computer.  
  
    -   Per analizzare istanze cluster, immettere il nome [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] virtuale.  
  
    -   Per analizzare i componenti non cluster installati in un nodo di un cluster, immettere il nome del nodo.  
  
    > [!WARNING]  
    >  Preparazione aggiornamento non supporta la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non sia impostata per utilizzare la porta standard (1433) per le connessioni client. Se si desidera connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non utilizza la porta standard (1433), creare un alias utilizzando l'indirizzo IP e la porta. Per ulteriori informazioni sulla configurazione dei protocolli client e sulla creazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un alias per le istanze, vedere [configure client Protocols](../../database-engine/configure-windows/configure-client-protocols.md).  
    >   
    >  Se non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è installato nel computer in cui si esegue Preparazione aggiornamento, fare clic su **Start**, quindi eseguire `cliconfg`. Verrà visualizzata la finestra di dialogo  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilità di rete client** . Utilizzare la scheda **alias** per creare l'alias.  
  
3.  Esaminare l'elenco dei componenti rilevati, modificare le selezioni secondo necessità e quindi fare clic su **Avanti**.  
  
4.  Nella pagina **parametri connessione** selezionare l'istanza di che si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desidera analizzare, selezionare il metodo di autenticazione e, se necessario, immettere le informazioni sul nome utente e la password e quindi fare clic su **Avanti**.  
  
     Il nome dell'istanza predefinita è MSSQLSERVER.  
  
5.  Per i componenti selezionati, immettere le informazioni richieste. Per ulteriori informazioni sulle singole finestre di dialogo, vedere Guida di [riferimento all'interfaccia utente di preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
6.  Nella pagina **Conferma impostazioni di preparazione aggiornamento** verificare le informazioni immesse. È possibile selezionare **Invia report a [!INCLUDE[msCoName](../../includes/msconame-md.md)]**  se si desidera inviare il report di aggiornamento. È inoltre possibile consultare l'informativa sulla privacy.  
  
7.  Fare clic su **Esegui** per analizzare l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]istanza di.  
  
8.  Al termine dell'analisi, fare clic su **Avvia report** per visualizzare i problemi di aggiornamento rilevati.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: Avvia preparazione aggiornamento](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Esecuzione dell'interfaccia &#40;utente di preparazione aggiornamento&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
