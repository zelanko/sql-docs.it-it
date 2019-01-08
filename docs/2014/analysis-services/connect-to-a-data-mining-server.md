---
title: Connettersi a un Server di Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
- getting started
ms.assetid: 85962ad6-d840-4bc6-905e-c667c3276944
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9ca50a030fef65c9de02bc93dcd970df2686b0a
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52420392"
---
# <a name="connect-to-a-data-mining-server"></a>Connessione al server di data mining
  ![Pulsante connessioni](media/misc-connection.gif "pulsante connessioni")  
  
 Scegliere il **Connection** pulsante per selezionare una connessione esistente oppure creare una nuova connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Il motivo per cui è necessario connettersi a un server?**  
  
 Quando si crea una connessione, è possibile utilizzare gli algoritmi di data mining forniti dal server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], nonché le funzionalità di elaborazione ottimizzate del server.  
  
 Non è necessario salvare i dati o i risultati in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o di SQL Server. I componenti aggiuntivi Data mining per Excel possono utilizzare i dati archiviati solo in Excel o i dati a cui è possibile connettersi come origine dati di Excel.  
  
## <a name="how-to-create-a-new-connection"></a>Modalità di creazione di una nuova connessione  
  
1.  Scegliere il **connessione** pulsante.  
  
2.  Nel **connessioni ad Analysis Services** finestra di dialogo, fare clic su **New**.  
  
3.  Nel **Connetti a Analysis Services** finestra di dialogo digitare un nome di server.  
  
4.  Specificare il metodo di autenticazione.  
  
5.  Specificare il catalogo o il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in cui verranno archiviati i modelli di data mining.  
  
    > [!NOTE]  
    >  Se non sono stati ancora creati database, è possibile utilizzare l'opzione (predefinito) per creare e quindi testare la connessione. Non è tuttavia possibile aggiungere modelli di data mining alla connessione predefinita. Prima di creare modelli di data mining, è necessario creare una connessione a un database esistente.  
  
6.  Se si esegue la connessione al server tramite un servizio Web, digitare il nome utente e la password necessari per il servizio Web.  
  
7.  Digitare un nome descrittivo per la nuova connessione.  
  
8.  Fare clic su **Test connessione** per verificare che il server è disponibile.  
  
## <a name="troubleshooting-connections"></a>Risoluzione dei problemi relativi alle connessioni  
 In questa sezione vengono fornite le risposte ad alcune domande frequenti sulle connessioni a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Viene visualizzato un messaggio "Nessuna connessione trovata."**  
  
 Se viene visualizzato il testo nella parte inferiore del pulsante **Nessuna connessione**, significa che non è stata creata una connessione a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] database oppure che la connessione non riesce. È possibile continuare a utilizzare i dati in Excel da Access o altre origini, ma per la creazione di un modello di data mining o l'esecuzione di una query di stima è necessaria una connessione attiva.  
  
 **Si supponga che non siamo autorizzati a usare il server?**  
  
 Se non si dispone di autorizzazioni sufficienti per archiviare i modelli di data mining nel server o si desidera provare a utilizzare il data mining senza salvare il lavoro svolto, è possibile utilizzare gli Strumenti di analisi tabelle che consentono di creare strutture dei dati o modelli temporanei. Sarà comunque necessario poter archiviare i modelli temporanei nel server. Chiedere all'amministratore di abilitare l'uso dei *modelli di data mining di sessione* nel server.  
  
 Per assicurarsi che i modelli vengano salvati, è possibile disabilitare l'opzione per l'utilizzo dei modelli temporanei o utilizzare le procedure guidate disponibili nel client di data mining. Queste procedure guidate archiviano tutti i modelli nel server. Poiché è necessario disporre dell'accesso amministrativo al database in cui vengono archiviati i modelli, è consigliabile chiedere all'amministratore di creare un database appositamente per la creazione di modelli di data mining con i componenti aggiuntivi.  
  
 **Ho perso la connessione. si perde anche il lavoro?**  
  
 Se si interrompe la connessione al server, i risultati e i dati non andranno persi perché sono archiviati in Excel. Tuttavia, se sono stati creati alcuni modelli temporanei, tali modelli verranno eliminati dal server dopo un breve periodo di tempo. Pertanto, se si perde temporaneamente la connessione, corrisponde a uno dei modelli non vengano eliminati.  
  
 I dati o i risultati generati non andranno persi, in quanto tutti i report e le tabelle sono archiviati in Excel.  
  
> [!NOTE]  
>  Non disconnettersi dal server o dalla rete durante la comunicazione dei componenti aggiuntivi con il server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Non disconnettersi mai, ad esempio, durante la creazione di un modello o l'elaborazione dei dati. In alcuni casi, questo potrebbe causare il danneggiamento dei dati.  
  
 **Non è possibile connettersi al modello utilizzando gli strumenti di Visio**  
  
 In Modelli di data mining per Visio non è possibile utilizzare modelli e strutture di data mining temporanei. Per creare un diagramma di un modello di data mining, è necessario che il modello sia archiviato in un server.  
  
 **Come è possibile monitorare l'utilizzo della connessione?**  
  
 Il [Trace &#40;Client di Data Mining per Excel&#41; ](trace-data-mining-client-for-excel.md) strumento crea un log di tutte le attività tra i componenti aggiuntivi e il server specificato.  
  
 Per abilitare il monitoraggio di modelli di sessione, selezionare la **Usa modelli di sessione** opzione il **traccia** nella finestra di dialogo.  
  
 Lo strumento Traccia consente di visualizzare i comandi DMX e XMLA generati al momento della creazione di modelli e strutture. È inoltre possibile visualizzare le query inviate dal client per generare i risultati e i report in Excel.  
  
 **Che cos'è un modello temporaneo? Come è possibile salvare un modello temporaneo?**  
  
 Per impostazione predefinita, gli Strumenti di analisi tabelle per Excel creano solo modelli di data mining e strutture dei dati temporanei. È possibile continuare a esplorare ed eseguire query sui modelli temporanei finché la cartella di lavoro rimane aperta e non viene disconnessa da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 I modelli e le strutture creati vengono eliminati non appena si chiude la cartella di lavoro di Excel oppure se si modifica o si termina la connessione ad [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Al termine della procedura guidata nel client di data mining per Excel, i modelli vengono salvati nel server per impostazione predefinita, ma nella pagina finale di ogni procedura guidata è presente l'opzione per utilizzare un modello temporaneo. Se si seleziona questa opzione, la struttura e il modello di data mining creati vengono archiviati in un file temporaneo. È possibile esplorare, gestire e modificare la struttura e il modello fino a quando Excel rimane aperto. Quando si chiude Excel, tuttavia, la struttura e i modelli correlati vengono eliminati.  
  
 È possibile creare in modo esplicito una struttura temporanea o un modello usando il **Editor avanzato Data Mining Query** e selezionando uno dei modelli DMX. Aggiungere la clausola `USE SESSION MODELS` per specificare che gli oggetti sono temporanei.   
  
### <a name="creating-backups-of-mining-models-and-structures"></a>Creazione di backup di strutture e modelli di data mining  
 Per creare un backup di un modello o struttura, è possibile esportarlo usando [Gestione modelli &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](manage-models-sql-server-data-mining-add-ins.md), nel Client di Data Mining per Excel.  
  
 Se è stato creato un modello di data mining temporaneo, in genere il nome assegnato è difficile da comprendere, ad esempio Table5_593679_TS_62446. Tuttavia, è possibile usare la [Trace &#40;Client di Data Mining per Excel&#41; ](trace-data-mining-client-for-excel.md) dello strumento per individuare i nomi delle strutture e modelli creati da strumenti di analisi tabelle temporanei e quindi eseguirne il backup usando  **Gestire i modelli**.  
  
##### <a name="identify-and-export-a-temporary-model"></a>Identificare ed esportare un modello temporaneo  
  
1.  Nel **connessioni** gruppo di Client di Data Mining per Excel, fare clic su **traccia**.  
  
2.  Visualizzare il log attività della connessione e individuare il modello controllando, ad esempio, le colonne e gli output stimabili.  
  
     Utenti avanzati: Se si ha familiarità con DMX o XMLA, è possibile copiare le istruzioni in un file per un uso successivo.  
  
3.  Dopo aver individuato il nome del modello temporaneo e struttura, aprire **Gestisci modelli** e selezionare il modello.  
  
4.  Fare clic su Esporta modello di data mining per generare un file script in un percorso specificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Connettersi all'origine dati &#40;Client di Data Mining per Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md)   
 [Utilità di configurazione server &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](server-configuration-utility-data-mining-add-ins-for-excel.md)  
  
  
