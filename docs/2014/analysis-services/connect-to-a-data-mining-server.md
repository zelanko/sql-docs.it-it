---
title: Connessione a un server di data mining | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
- getting started
ms.assetid: 85962ad6-d840-4bc6-905e-c667c3276944
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3c9abd1b891d47f1711db21eec017ec755526e02
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087350"
---
# <a name="connect-to-a-data-mining-server"></a>Connessione al server di data mining
  ![Pulsante Connessioni](media/misc-connection.gif "Pulsante Connessioni")  
  
 Fare clic sul pulsante **connessione** per selezionare una connessione esistente o per creare una nuova connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Perché è necessario connettersi a un server?**  
  
 Quando si crea una connessione, è possibile utilizzare gli algoritmi di data mining forniti dal server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], nonché le funzionalità di elaborazione ottimizzate del server.  
  
 Non è necessario salvare i dati o i risultati in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o di SQL Server. I componenti aggiuntivi Data mining per Excel possono utilizzare i dati archiviati solo in Excel o i dati a cui è possibile connettersi come origine dati di Excel.  
  
## <a name="how-to-create-a-new-connection"></a>Modalità di creazione di una nuova connessione  
  
1.  Fare clic sul pulsante **connessione** .  
  
2.  Nella finestra di dialogo **Analysis Services connessioni** fare clic su **nuovo**.  
  
3.  Nella finestra di dialogo **Connetti a Analysis Services** Digitare un nome di server.  
  
4.  Specificare il metodo di autenticazione.  
  
5.  Specificare il catalogo o il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in cui verranno archiviati i modelli di data mining.  
  
    > [!NOTE]  
    >  Se non sono stati ancora creati database, è possibile utilizzare l'opzione (predefinito) per creare e quindi testare la connessione. Non è tuttavia possibile aggiungere modelli di data mining alla connessione predefinita. Prima di creare modelli di data mining, è necessario creare una connessione a un database esistente.  
  
6.  Se si esegue la connessione al server tramite un servizio Web, digitare il nome utente e la password necessari per il servizio Web.  
  
7.  Digitare un nome descrittivo per la nuova connessione.  
  
8.  Fare clic su **Test connessione** per verificare che il server sia disponibile.  
  
## <a name="troubleshooting-connections"></a>Risoluzione dei problemi relativi alle connessioni  
 In questa sezione vengono fornite le risposte ad alcune domande frequenti sulle connessioni a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Viene ricevuto un messaggio che informa che non è stata trovata alcuna connessione.**  
  
 Se il testo nella parte inferiore del pulsante **non indica alcuna connessione**, significa che non è stata creata una connessione a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] database o che la connessione non è riuscita. È possibile continuare a utilizzare i dati in Excel da Access o altre origini, ma per la creazione di un modello di data mining o l'esecuzione di una query di stima è necessaria una connessione attiva.  
  
 **Si supponga che non si disponga dell'autorizzazione per utilizzare il server?**  
  
 Se non si dispone di autorizzazioni sufficienti per archiviare i modelli di data mining nel server o si desidera provare a utilizzare il data mining senza salvare il lavoro svolto, è possibile utilizzare gli Strumenti di analisi tabelle che consentono di creare strutture dei dati o modelli temporanei. Sarà comunque necessario poter archiviare i modelli temporanei nel server. Richiedere all'amministratore di abilitare l'utilizzo dei *modelli di data mining di sessione* nel server.  
  
 Per assicurarsi che i modelli vengano salvati, è possibile disabilitare l'opzione per l'utilizzo dei modelli temporanei o utilizzare le procedure guidate disponibili nel client di data mining. Queste procedure guidate archiviano tutti i modelli nel server. Poiché è necessario disporre dell'accesso amministrativo al database in cui vengono archiviati i modelli, è consigliabile chiedere all'amministratore di creare un database appositamente per la creazione di modelli di data mining con i componenti aggiuntivi.  
  
 **Se si perde la connessione, si perde anche il lavoro?**  
  
 Se si interrompe la connessione al server, i risultati e i dati non andranno persi perché sono archiviati in Excel. Tuttavia, se sono stati creati alcuni modelli temporanei, tali modelli verranno eliminati dal server dopo un breve periodo di tempo. Quindi, se la connessione viene persa temporaneamente, a volte i modelli non verranno ancora eliminati.  
  
 I dati o i risultati generati non andranno persi, in quanto tutti i report e le tabelle sono archiviati in Excel.  
  
> [!NOTE]  
>  Non disconnettersi dal server o dalla rete durante la comunicazione dei componenti aggiuntivi con il server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Non disconnettersi mai, ad esempio, durante la creazione di un modello o l'elaborazione dei dati. In alcuni casi, questo potrebbe causare il danneggiamento dei dati.  
  
 **Impossibile connettersi al modello mediante gli strumenti di Visio**  
  
 In Modelli di data mining per Visio non è possibile utilizzare modelli e strutture di data mining temporanei. Per creare un diagramma di un modello di data mining, è necessario che il modello sia archiviato in un server.  
  
 **Come è possibile monitorare l'utilizzo della connessione?**  
  
 Lo strumento [Trace &#40;data mining client for Excel&#41;](trace-data-mining-client-for-excel.md) crea un log di tutte le attività tra i componenti aggiuntivi e il server specificato.  
  
 Per abilitare il monitoraggio dei modelli di sessione, selezionare l'opzione **Usa modelli di sessione** nella finestra di dialogo utilità di **traccia** .  
  
 Lo strumento Traccia consente di visualizzare i comandi DMX e XMLA generati al momento della creazione di modelli e strutture. È inoltre possibile visualizzare le query inviate dal client per generare i risultati e i report in Excel.  
  
 **Che cos'è un modello temporaneo? Come è possibile salvare un modello temporaneo?**  
  
 Per impostazione predefinita, gli Strumenti di analisi tabelle per Excel creano solo modelli di data mining e strutture dei dati temporanei. È possibile continuare a esplorare ed eseguire query sui modelli temporanei finché la cartella di lavoro rimane aperta e non viene disconnessa da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 I modelli e le strutture creati vengono eliminati non appena si chiude la cartella di lavoro di Excel oppure se si modifica o si termina la connessione ad [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Al termine della procedura guidata nel client di data mining per Excel, i modelli vengono salvati nel server per impostazione predefinita, ma nella pagina finale di ogni procedura guidata è presente l'opzione per utilizzare un modello temporaneo. Se si seleziona questa opzione, la struttura e il modello di data mining creati vengono archiviati in un file temporaneo. È possibile esplorare, gestire e modificare la struttura e il modello fino a quando Excel rimane aperto. Quando si chiude Excel, tuttavia, la struttura e i modelli correlati vengono eliminati.  
  
 È inoltre possibile creare in modo esplicito una struttura o un modello temporaneo utilizzando l' **Editor avanzato query di data mining** e selezionando uno dei modelli DMX. Aggiungere la clausola `USE SESSION MODELS` per specificare che gli oggetti sono temporanei.   
  
### <a name="creating-backups-of-mining-models-and-structures"></a>Creazione di backup di strutture e modelli di data mining  
 Per creare un backup di un modello o di una struttura, è possibile esportarlo utilizzando [Gestisci modelli &#40;SQL Server componenti aggiuntivi Data mining&#41;](manage-models-sql-server-data-mining-add-ins.md)nel client di data mining per Excel.  
  
 Se è stato creato un modello di data mining temporaneo, in genere il nome assegnato è difficile da comprendere, ad esempio Table5_593679_TS_62446. Tuttavia, è possibile utilizzare lo strumento [traccia &#40;client di data mining per&#41;Excel](trace-data-mining-client-for-excel.md) per individuare i nomi delle strutture e dei modelli temporanei creati dagli strumenti di analisi tabelle, quindi eseguirne il backup utilizzando **Gestisci modelli**.  
  
##### <a name="identify-and-export-a-temporary-model"></a>Identificare ed esportare un modello temporaneo  
  
1.  Nel gruppo **connessioni** del client di data mining per Excel fare clic su **traccia**.  
  
2.  Visualizzare il log attività della connessione e individuare il modello controllando, ad esempio, le colonne e gli output stimabili.  
  
     Utenti avanzati: se si ha familiarità con DMX o XMLA, è possibile copiare le istruzioni in un file per un utilizzo futuro.  
  
3.  Dopo aver individuato il nome del modello e della struttura temporanei, aprire **Gestisci modello** e selezionare il modello.  
  
4.  Fare clic su Esporta modello di data mining per generare un file script in un percorso specificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Connettersi ai dati di origine &#40;client di data mining per Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md)   
 [Utilità di configurazione del server &#40;componenti aggiuntivi Data mining per Excel&#41;](server-configuration-utility-data-mining-add-ins-for-excel.md)  
  
  
