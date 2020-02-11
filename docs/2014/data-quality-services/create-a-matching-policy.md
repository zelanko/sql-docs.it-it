---
title: Creare criteri di corrispondenza | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.kbmatchingresults.f1
- sql12.dqs.kb.kbmatchingmap.f1
- sql12.dqs.kb.kbmatchingpolicy.f1
ms.assetid: cce77a06-ca31-47b6-8146-22edf001d605
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f0623f79c3d17f3e350c151d64bb00372e3ffe56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65481018"
---
# <a name="create-a-matching-policy"></a>Creazione di criteri di corrispondenza
  In questo argomento viene descritto come creare dei criteri di corrispondenza in una Knowledge Base di [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). La preparazione del processo di corrispondenza in DQS si effettua eseguendo l'attività dei criteri di corrispondenza su dati di esempio. In tale attività vengono create e testate una o più regole di corrispondenza nei criteri, quindi viene pubblicata la Knowledge Base per rendere le regole di corrispondenza pubblicamente disponibili per l'uso. In una Knowledge Base può essere presente solo un set di criteri di corrispondenza, ma tali criteri possono contenere più regole di corrispondenza.  
  
 La creazione di criteri di corrispondenza viene eseguita in tre fasi: un processo di mapping nel quale si identifica l'origine dati e si esegue il mapping dei domini alle colonne; un processo per i criteri di corrispondenza nel quale si creano una o più regole di corrispondenza e si esegue separatamente il testing di ciascuna regola; un processo per i risultati di corrispondenza nel quale vengono eseguite tutte le regole insieme e, una volta confermate, si aggiungono i relativi criteri alla Knowledge Base. Ognuno di questi processi viene eseguito in una pagina separata della procedura guidata relativa all'attività dei criteri di corrispondenza, consentendo all'utente di spostarsi da una pagina a un'altra al fine di rieseguire il processo, di completare un processo specifico relativo ai criteri di corrispondenza e di tornare nuovamente alla stessa fase del processo. Dopo avere testato tutte le regole insieme, è possibile tornare alla pagina **Criteri di corrispondenza** , modificare una regola specifica, testarla di nuovo separatamente, quindi tornare alla pagina **Risultati corrispondenza** per eseguire nuovamente tutte le regole insieme. DQS fornisce statistiche relative ai dati di origine, alle regole e ai risultati di corrispondenza. Tali statistiche consentono di prendere decisioni informate sui criteri di corrispondenza, agevolandone la modifica.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Se i dati di origine si trovano in un file di Excel, è necessario che Microsoft Excel sia installato nel computer [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . In caso contrario, non sarà possibile selezionare il file di Excel nella fase di mapping. I file creati da Microsoft Excel potranno presentare l'estensione xlsx, xls o csv. Se viene utilizzata la versione a 64 bit di Excel, sono supportati solo i file di Excel 2003 (xls), mentre non sono supportati file di Excel 2007 o 2010 (xlsx). Se si utilizza una versione a 64 bit di Excel 2007 o 2010, salvare il file come file xls o csv o installare una versione a 32 bit di Excel.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per creare i criteri di corrispondenza, è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="MatchingRules"></a>Come impostare i parametri della regola di corrispondenza  
 La creazione di una regola di corrispondenza è un processo iterativo nel quale si immettono i fattori utilizzati per determinare se un record corrisponde a un altro. È possibile immettere in una tabella condizioni applicabili a qualsiasi dominio. Quando in DQS viene eseguita l'individuazione della corrispondenza tra due record, vengono confrontati i valori nei campi di cui è stato eseguito il mapping ai domini inclusi nella regola di corrispondenza. Vengono analizzati i valori in ogni campo nella regola, quindi vengono utilizzati i fattori immessi nella regola per ciascun dominio per calcolare un punteggio di corrispondenza finale. Se il punteggio di corrispondenza per i due record confrontati è maggiore del punteggio di corrispondenza minimo, i due campi verranno considerati corrispondenti.  
  
 I fattori che si immettono in una regola di corrispondenza includono gli elementi seguenti:  
  
-   Peso: per ogni dominio nella regola, immettere un valore numerico che verrà utilizzato per determinare la modalità di confronto della corrispondenza analizzata per quel dominio con il valore corrispondente a ciascun altro dominio nella regola. Il peso indica il contributo del punteggio del campo al punteggio di corrispondenza complessivo tra due record. I punteggi calcolati assegnati a ciascun campo di origine vengono sommati insieme per ottenere un punteggio di corrispondenza composito per i due record. Per ciascun campo che non rappresenti un prerequisito (con una somiglianza esatta o simile), impostare il peso tra 10 e 100. La somma dei pesi dei domini che non sono prerequisiti deve essere pari a 100. Se il valore è un prerequisito, il peso viene impostato su 0 e non è possibile modificarlo.  
  
-   Somiglianza esatta: selezionare **Esatta** se i valori nello stesso campo di due record diversi devono essere identici affinché i valori vengano considerati corrispondenti. Se sono identici, il punteggio di corrispondenza per quel dominio verrà impostato su "100" e verrà utilizzato in DQS insieme ai punteggi per gli altri domini nella regola per determinare il punteggio di corrispondenza aggregato. Se non sono identici, il punteggio di corrispondenza per quel dominio verrà impostato su "0" e l'elaborazione della regola proseguirà passando alla condizione successiva. Se si imposta una regola di corrispondenza per un dominio numerico e si seleziona **Simile**, è possibile immettere una tolleranza come percentuale o come numero intero. Se si seleziona **Simile**per un dominio di tipo data, è possibile immettere una tolleranza come giorno, mese o anno (numero intero). Non è prevista l'immissione di una percentuale per un dominio di tipo data. L'opzione non è disponibile se si seleziona **Esatta**.  
  
-   Somiglianza simile: selezionare **Simile** se due valori nello stesso campo di due record diversi possono essere considerati corrispondenti anche se tali valori non sono identici. Durante l'esecuzione della regola in DQS, viene calcolato il punteggio di corrispondenza per quel dominio e tale punteggio viene utilizzato insieme ai punteggi per gli altri domini nella regola per determinare il punteggio di corrispondenza aggregato. La somiglianza minima tra i valori di un campo è 60%. Se il punteggio di corrispondenza calcolato per un campo di due record è minore di 60, il punteggio di somiglianza viene impostato automaticamente su 0. Se si imposta una regola di corrispondenza per un campo numerico e si seleziona **Simile**, è possibile immettere una tolleranza come percentuale o come numero intero. Se si imposta una regola di corrispondenza per un campo data e si seleziona **Simile**, è possibile immettere una tolleranza numerica.  
  
-   Prerequisito: selezionare **Prerequisito** per specificare che i valori nello stesso campo in due record diversi devono restituire una corrispondenza del 100% e che, in caso contrario, i record non devono essere considerati corrispondenti e le altre clausole nella regola devono essere ignorate. Quando si seleziona **Prerequisito** , il campo relativo al peso per il dominio viene rimosso in modo che non sia possibile definire alcun peso per il dominio. Sarà necessario reimpostare il peso di uno o più domini in modo che la somma dei pesi sia uguale a 100. I domini prerequisiti non contribuiscono al punteggio di corrispondenza dei record. Il punteggio di corrispondenza dei record viene determinato confrontando i valori nei campi per i quali la somiglianza è impostata su Simile o Esatta. Quando si rende un campo prerequisito, la somiglianza per quel dominio viene impostata automaticamente su Esatta.  
  
 Il punteggio di corrispondenza minimo è la soglia a cui, od oltre cui, due record vengono considerati corrispondenti (lo stato per tali record viene impostato su "Con corrispondenza"). Immettere un valore intero in incrementi di 1 o fare clic sulla freccia Su o Giù per aumentare o diminuire il valore in incrementi di 10. Il valore minimo è 80. Se il punteggio di corrispondenza è inferiore a 80, i due record non vengono considerati corrispondenti. Non è possibile modificare l'intervallo del punteggio di corrispondenza minimo in questa pagina. Il punteggio di corrispondenza minimo più basso è pari a 80. Se si è un amministratore DQS, tuttavia, è possibile modificare il punteggio di corrispondenza minimo più basso nella pagina Amministrazione.  
  
 La creazione di una regola di corrispondenza è un processo iterativo perché nella regola stessa potrebbe essere necessario modificare i pesi relativi dei domini, la somiglianza o la proprietà di prerequisito per un dominio oppure il punteggio di corrispondenza minimo per la regola, al fine di realizzare i risultati attesi. È inoltre possibile che si debbano creare più regole, ognuna delle quali verrà eseguita per creare il punteggio di corrispondenza. Ottenere il risultato previsto con una sola regola potrebbe risultare difficile, mentre con più regole si otterranno visualizzazioni diverse di una corrispondenza richiesta. Mediante l'utilizzo di più regole è possibile includere meno domini in ogni regola, utilizzare pesi superiori per ogni dominio e ottenere risultati migliori. Se i dati sono meno accurati e completi, potrebbe essere necessario un numero maggiore di regole per trovare le corrispondenze richieste. Se i dati sono più accurati e completi, saranno necessarie meno regole.  
  
 Il profiling fornisce informazioni essenziali quanto a completezza e univocità. Completezza e univocità sono qualità da prendere in considerazione in parallelo. Utilizzare i dati di completezza e univocità per determinare il peso da assegnare a un campo nel processo di corrispondenza. Se vi è un livello elevato di univocità in un campo, l'utilizzo di tale campo nei criteri di corrispondenza può ridurre il numero di risultati di corrispondenza, pertanto è consigliabile impostare il peso per il campo su un valore relativamente basso. Se si dispone di un basso livello di univocità per una colonna, ma anche di un basso livello di completezza, non è consigliabile includere un dominio per tale colonna. Con un basso livello di univocità, ma un elevato livello di completezza, è consigliabile includere il dominio. È possibile che alcune colonne, ad esempio di tipo genere, forniscano naturalmente un basso livello di univocità. Per altre informazioni, vedere [Schede Profiler e Risultati](#Tabs).  
  
##  <a name="Starting"></a>Primo passaggio: avvio di criteri di corrispondenza  
 L'attività relativa ai criteri di corrispondenza viene eseguita nell'area di gestione della Knowledge Base dell'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] fare clic su **Nuova Knowledge Base** per creare i criteri di corrispondenza in una nuova Knowledge Base. Immettere un nome per la Knowledge Base, una descrizione, quindi impostare **Crea Knowledge Base da** sull'opzione desiderata. Fare clic su **Criteri di corrispondenza** per l'attività. Fare clic su **Avanti** per continuare.  
  
3.  Fare clic su **Apri Knowledge Base** per creare o modificare i criteri di corrispondenza in una Knowledge Base esistente. Selezionare la Knowledge Base, selezionare **Criteri di corrispondenza**, quindi fare clic su **Avanti**. È anche possibile fare clic su una Knowledge Base in **Knowledge Base recente**. Se si apre una Knowledge Base chiusa mentre erano in esecuzione dei criteri di corrispondenza, si procederà con la fase in cui tale attività era stata chiusa (come indicato dalla colonna **Stato** per la Knowledge Base nella relativa tabella o nel nome della Knowledge Base visualizzato in **Knowledge Base recente**). Se si apre una Knowledge Base che include criteri di corrispondenza e che è stata completata, si passerà alla pagina **Criteri di corrispondenza** . Se si apre una Knowledge Base che non include criteri di corrispondenza e che è stata completata, si passerà alla pagina **Mapping** .  
  
##  <a name="MatchingStage"></a>Fase di mapping  
 Nella fase di mapping si identifica l'origine dei dati per i quali verranno creati criteri di corrispondenza e si esegue il mapping delle colonne di origine ai domini per rendere tali domini disponibili per l'attività relativa ai criteri di corrispondenza.  
  
1.  Nella pagina **Mappa** , per creare criteri per un database, lasciare **Origine dati** come **SQL Server**, selezionare il database per il quale si desidera creare i criteri in **Database**, quindi selezionare la tabella o vista in **Tabella/Vista**. Il database di origine deve trovarsi nella stessa istanza di SQL Server di [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], in caso contrario, non verrà visualizzato nell'elenco a discesa.  
  
2.  Per creare criteri per i dati in un foglio di calcolo di Excel, selezionare **File di Excel** come **Origine dati**, fare clic su **Sfoglia** e selezionare il file di Excel, quindi lasciare selezionato **Utilizza la prima riga come intestazione** , se appropriato. In **Foglio di lavoro**selezionare il foglio di lavoro nel file di Excel che fungerà da origine dei dati. Per selezionare un file di Excel, è necessario che Microsoft Excel sia installato nel computer Data Quality Client. In caso contrario, il pulsante Sfoglia non sarà disponibile e verrà visualizzata una notifica sotto questa casella di testo in cui si avvisa che Microsoft Excel non è installato.  
  
3.  In **Mapping**, selezionare un campo per **Colonna di origine**, quindi fare clic sull'icona **Crea dominio** .  
  
4.  In **Mapping**, selezionare un campo nell'origine dati per **Colonna di origine**, quindi selezionare il dominio corrispondente. Ripetere l'operazione per tutti i domini da utilizzare per il processo di corrispondenza. Creare i domini necessari facendo clic su **Crea un Dominio** o su **Crea un dominio composito**.  
  
    > [!NOTE]  
    >  È possibile eseguire il mapping dei dati di origine a un dominio DQS durante la creazione di criteri di corrispondenza solo se il tipo di dati di origine è supportato in DQS e corrisponde al tipo di dati del dominio DQS. Per ulteriori informazioni sui tipi di dati supportati in DQS, vedere [Tipi di dati di SQL Server e SSIS supportati per i domini DQS](../../2014/data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
5.  Fare clic sul controllo **Più (+)** per aggiungere una riga alla tabella Mapping o sul controllo **Meno (-)** per rimuovere una riga.  
  
6.  Fare clic su **Anteprima origine dati** per visualizzare i dati nella tabella o vista di SQL Server selezionata o nel foglio di lavoro di Excel selezionato.  
  
7.  Fare clic su **Visualizza/Seleziona domini compositi** per visualizzare un elenco dei domini compositi disponibili nella Knowledge Base e selezionarli in base alle esigenze per l'esecuzione del mapping.  
  
8.  Fare clic su **Avanti** per passare alla fase di esecuzione dei criteri di corrispondenza.  
  
    > [!NOTE]  
    >  Fare clic su **Chiudi** per salvare la fase del progetto di corrispondenza e tornare alla home page di DQS. Alla successiva apertura, il progetto verrà avviato dalla stessa fase. Fare clic su **Annulla** per terminare l'attività di corrispondenza e tornare alla home page di DQS.  
  
##  <a name="MatchingPolicyStage"></a>Fase dei criteri di corrispondenza  
 Vengono create regole di corrispondenza che vengono testate individualmente nella pagina Criteri di corrispondenza. Quando si testa una regola di corrispondenza sulla pagina **Criteri di corrispondenza** , viene visualizzata una tabella dei risultati di corrispondenza in cui sono mostrati i cluster identificati da DQS per la regola selezionata. Nella tabella viene visualizzato ciascun record nel cluster con i valori del dominio di mapping, il punteggio di corrispondenza e il record pivot iniziale per il cluster. È inoltre possibile visualizzare i dati di profiling per il processo di corrispondenza nel suo insieme, le condizioni in ogni regola di corrispondenza e statistiche sui risultati separate per ciascuna regola di corrispondenza. È possibile impostare un filtro sui dati relativi alle regole master desiderate.  
  
 Per ulteriori informazioni sul funzionamento delle regole di corrispondenza, vedere [Modalità di impostazione dei parametri relativi alle regole di corrispondenza](#MatchingRules).  
  
1.  Nella pagina **Criteri di corrispondenza** fare clic sull'icona **Crea regola di corrispondenza** .  
  
2.  Immettere un nome e una descrizione per la regola.  
  
3.  Aumentare il valore del **Punteggio corrispondente minimo** se si desidera rendere più severi i requisiti di corrispondenza. Per ulteriori informazioni sul punteggio di corrispondenza minimo, vedere [Modalità di impostazione dei parametri relativi alle regole di corrispondenza](#MatchingRules).  
  
4.  Fare clic sull'icona **Aggiungi nuovo elemento di dominio** .  
  
5.  Selezionare un dominio o un dominio composito per il quale immettere i valori.  
  
    > [!NOTE]  
    >  È possibile selezionare un dominio composito solo se per ciascun dominio al suo interno è stato eseguito il mapping a una colonna di origine.  
  
6.  Selezionare **Simile**come **Somiglianza** se due valori nello stesso campo di due record diversi possono essere considerati corrispondenti anche se non identici. Selezionare **Esatta** se due valori nello stesso campo di due record diversi devono essere identici per essere considerati corrispondenti. (Per altre informazioni, vedere [Modalità di impostazione dei parametri relativi alle regole di corrispondenza](#MatchingRules).)  
  
7.  Per **Peso**, immettere un valore che determina il contributo del punteggio di corrispondenza di un dominio a quello complessivo per due record.  
  
    > [!NOTE]  
    >  Quando si definisce un peso per un dominio composito, è possibile immettere un peso diverso per ogni singolo dominio in tale dominio composito, nel qual caso non verrà ad esso assegnato un peso proprio, oppure è possibile immettere un singolo peso per il dominio composito, nel qual caso non vengono assegnati pesi individuali ai singoli domini che ne formano parte.  
  
8.  Selezionare **Prerequisito** per specificare che i valori per il campo in due record diversi deve restituire una corrispondenza del 100% e che, in caso contrario, i record non devono essere considerati corrispondenti e le altre clausole nella regola devono essere ignorate. Se la **Somiglianza** è **Simile**, verrà modificata in **Esatta**e il peso verrà rimosso, poiché la corrispondenza deve essere pari al 100%.  
  
9. Ripetere passaggi da 4 a 8 per tutti gli altri domini che faranno parte della regola di corrispondenza. Assicurarsi che la somma dei pesi per tutti i domini nella regola sia uguale a 100.  
  
10. Selezionare **Cluster sovrapposti** dall'elenco a discesa per visualizzare i record pivot e i record successivi per tutti i cluster quando viene eseguita la corrispondenza, anche qualora i gruppi di cluster presentino record in comune. Selezionare **Cluster non sovrapposti** per visualizzare i cluster che presentano record in comune come cluster singolo all'esecuzione della corrispondenza.  
  
11. Fare clic su **Ricarica dati di origine** per copiare i dati dall'origine dati nella tabella di staging e reindicizzarli quando si eseguono i criteri di corrispondenza. Fare clic su **Esegui sui dati precedenti** per eseguire i criteri di corrispondenza senza copiare i dati nella tabella di staging e senza reindicizzare i dati. **Esegui sui dati precedenti** è disabilitato per la prima esecuzione dei criteri di corrispondenza o se si modifica il mapping nella pagina **Mappa** e si preme **Sì** nel popup seguente. In entrambi tali casi, è necessario effettuare la reindicizzazione. Se i criteri di corrispondenza non vengono modificati, non è necessaria alcuna reindicizzazione. L'esecuzione sui dati precedenti può migliorare le prestazioni.  
  
12. Fare clic su **Start** per avviare il processo di corrispondenza per la regola selezionata. Una volta completato il processo, nella tabella viene visualizzato l'ID del record, il numero del cluster e delle colonne di dati (incluse quelle non presenti nella regola di corrispondenza) per ciascun record in un cluster. La riga pivot nel cluster è considerata il candidato principale per il superamento del processo di deduplicazione. Ogni riga aggiuntiva in un cluster è considerata un duplicato; il punteggio di corrispondenza (confrontato con il record pivot) è riportato nella tabella dei risultati. Il numero del cluster corrisponde all'ID record relativo al record pivot nel cluster.  
  
13. È possibile lavorare con i dati nella tabella **Risultati corrispondenza** come indicato di seguito:  
  
    -   In **Filtro**selezionare **Con corrispondenza** per visualizzare tutte le righe con corrispondenza e il relativo punteggio. Le righe che non vengono considerate corrispondenze (cioè che presentano un punteggio di corrispondenza inferiore a quello minimo) non vengono visualizzate nella tabella dei risultati di corrispondenza. Selezionare **Senza corrispondenza** per visualizzare tutte le righe non corrispondenti e non quelle corrispondenti.  
  
    -   Nella casella di riepilogo a discesa **Percentuale** selezionare una percentuale dall'elenco in incrementi di 5. Tutte le righe con un punteggio di corrispondenza maggiore o uguale a tale percentuale verranno visualizzate nella tabella dei risultati di corrispondenza.  
  
    -   Se si fa doppio clic su un record nella tabella dei risultati di corrispondenza, in DQS viene visualizzata la schermata popup **Dettagli punteggio corrispondente** in cui sono visibili il record pivot e il record di origine (nonché i valori in tutti i relativi campi), il punteggio tra tali record e un drill-down della loro corrispondenza. Nel drill-down vengono visualizzati i valori in ogni campo del record pivot e del record di origine, in modo da poterli confrontare, e il punteggio di corrispondenza tramite cui ogni campo contribuisce al punteggio di corrispondenza complessivo per i due record.  
  
14. Visualizzare le statistiche nelle schede **Profiler** e **Risultati corrispondenza** per assicurarsi che si stiano ottenendo i risultati desiderati. Per altre informazioni, vedere [Schede Profiler e Risultati](#Tabs).  
  
15. Se sono necessarie modifiche alla regola, modificarla nell'Editor Regole e fare clic su **Riavvia**.  
  
    > [!NOTE]  
    >  Una volta completata la prima analisi dei dati, il pulsante **Avvia** viene sostituito dal pulsante **Riavvia** . Se i risultati dall'analisi precedente non sono stati ancora salvati, facendo clic su **Riavvia** si causerà la perdita di tali dati non salvati. Durante l'esecuzione dell'analisi, non lasciare la pagina o il processo di analisi verrà interrotto.  
  
16. Nella scheda **Risultati corrispondenza** vengono visualizzate le statistiche per le ultime due esecuzioni della regola. Se la regola di corrispondenza è stata eseguita più di una volta con impostazioni diverse, confrontare le statistiche relative alla regola corrente con quelle della regola precedente. Se i risultati dalla regola precedente sono migliori, fare clic su **Ripristina regola precedente** per ripristinare le condizioni della regola precedente e riportarla allo stato precedente la modifica. Le condizioni della regola correnti andranno perse. Questa procedura consente di ottimizzare i criteri in base alle ultime due esecuzioni del processo, diminuendo i tempi necessari per l'ottimizzazione dei criteri di corrispondenza.  
  
17. Se si desidera aggiungere un'altra regola ai criteri di corrispondenza, ripetere i passaggi iniziando dal passaggio 1.  
  
18. Fare clic su **Avanti** per passare alla fase relativa ai risultati di corrispondenza.  
  
##  <a name="MatchingResultsStage"></a>Fase Risultati corrispondenza  
 Il testing di tutte le regole di corrispondenza viene eseguito nella pagina **Risultati corrispondenza** . Prima di procedere, è possibile specificare che durante l'esecuzione dei test della regola vengano identificati i cluster sovrapposti e quelli non sovrapposti. Se si eseguono le regole più volte, è possibile eseguire la regola sui dati ricaricati dall'origine o sui dati precedenti.  
  
 Quando si testano le regole di corrispondenza nella pagina **Risultati corrispondenza** , viene visualizzata una tabella dei risultati di corrispondenza in cui sono visualizzati i cluster identificati da DQS per tutte le regole. Nella tabella viene visualizzato ciascun record nel cluster con i valori del dominio di mapping, il punteggio di corrispondenza e il record pivot iniziale per il cluster. È inoltre possibile visualizzare i dati di profiling per le regole di corrispondenza nel loro insieme, le condizioni in ogni regola di corrispondenza e statistiche sui risultati per tutte le regole di corrispondenza.  
  
1.  Nella pagina **Risultati corrispondenza** selezionare **Cluster sovrapposti** dall'elenco a discesa per visualizzare i record pivot e i record successivi per tutti i cluster quando viene eseguita la corrispondenza, anche qualora i gruppi di cluster presentino record in comune. Selezionare **Cluster non sovrapposti** per visualizzare i cluster che presentano record in comune come cluster singolo all'esecuzione della corrispondenza.  
  
2.  Fare clic su **Ricarica dati di origine** per copiare i dati dall'origine dati nella tabella di staging e reindicizzarli quando si eseguono i criteri di corrispondenza. Fare clic su **Esegui sui dati precedenti** per eseguire i criteri di corrispondenza senza copiare i dati nella tabella di staging e senza reindicizzare i dati. **Esegui sui dati precedenti** è disabilitato per la prima esecuzione dei criteri di corrispondenza o se si modifica il mapping nella pagina **Mappa** e si preme **Sì** nel popup seguente. In entrambi tali casi, è necessario effettuare la reindicizzazione. Se i criteri di corrispondenza non vengono modificati, non è necessaria alcuna reindicizzazione. L'esecuzione sui dati precedenti può migliorare le prestazioni.  
  
3.  Fare clic su **Avvia** per eseguire il processo di corrispondenza per tutte le regole definite. Nella tabella **Risultati corrispondenza** viene visualizzato l'ID del record, il numero del cluster e delle colonne di dati (incluse quelle non presenti nella regola di corrispondenza) per ciascun record in un cluster. Il record iniziale nel cluster viene selezionato casualmente. Il record superstite viene determinato selezionando la regola di sopravvivenza nella pagina **Esporta** quando si esegue il progetto corrispondente. Ogni riga aggiuntiva in un cluster è considerata un duplicato; Il Punteggio corrispondente (rispetto al record pivot) viene fornito nella tabella dei risultati.  
  
4.  È possibile lavorare con i dati nella tabella **Risultati corrispondenza** come indicato di seguito:  
  
    -   In **Filtro**selezionare **Con corrispondenza** per visualizzare tutte le righe con corrispondenza e il relativo punteggio. Le righe che non vengono considerate corrispondenze (cioè che presentano un punteggio di corrispondenza inferiore a quello minimo) non vengono visualizzate nella tabella dei risultati di corrispondenza. Selezionare **Senza corrispondenza** per visualizzare tutte le righe non corrispondenti e non quelle corrispondenti.  
  
    -   Nella casella di riepilogo a discesa **Percentuale** selezionare una percentuale dall'elenco in incrementi di 5. Tutte le righe con un punteggio di corrispondenza maggiore o uguale a tale percentuale verranno visualizzate nella tabella dei risultati di corrispondenza.  
  
    -   Se si fa doppio clic su un record nella tabella dei risultati di corrispondenza, in DQS viene visualizzata la schermata popup **Dettagli punteggio corrispondente** in cui sono visibili il record pivot e il record di origine (nonché i valori in tutti i relativi campi), il punteggio tra tali record e un drill-down della loro corrispondenza. Nel drill-down vengono visualizzati i valori in ogni campo del record pivot e del record di origine, in modo da poterli confrontare, e il punteggio di corrispondenza tramite cui ogni campo contribuisce al punteggio di corrispondenza complessivo per i due record.  
  
5.  Visualizzare le statistiche nelle schede **Profiler** e **Risultati corrispondenza** per assicurarsi che si stiano ottenendo i risultati desiderati. Fare clic sulla scheda **Regole di corrispondenza** per verificare le impostazioni di dominio per ciascuna regola. Per altre informazioni, vedere [Schede Profiler e Risultati](#Tabs).  
  
6.  Se non si è soddisfatti dei risultati di tutte le regole, fare clic su **Indietro** per tornare alla pagina **Criteri di corrispondenza** , modificare una o più regole come desiderato, tornare alla pagina **Risultati corrispondenza** , quindi fare clic su **Riavvia**.  
  
    > [!NOTE]  
    >  Una volta completata l'analisi, il pulsante **Avvia** viene sostituito dal pulsante **Riavvia** . Se i risultati dall'analisi precedente non sono stati ancora salvati, facendo clic su **Riavvia** si causerà la perdita di tali dati non salvati.  
  
7.  Se si è soddisfatti dei risultati di tutte le regole, fare clic su **Fine** per completare il processo per i criteri di corrispondenza, quindi fare clic su uno degli elementi seguenti:  
  
    -   **Sì-pubblica la Knowledge base e Chiudi**: la Knowledge base verrà pubblicata per l'uso da parte dell'utente corrente o di altri utenti. La Knowledge Base non verrà bloccata, lo stato della Knowledge Base nella relativa tabella verrà impostato come vuoto e saranno disponibili entrambe le attività, Gestione dominio e Individuazione informazioni. Verrà di nuovo visualizzata la schermata Apri Knowledge Base.  
  
    -   **No-Salva il lavoro sulla Knowledge base e Chiudi**: il lavoro verrà salvato, la Knowledge base rimarrà bloccata e lo stato della Knowledge base verrà impostato su **in lavorazione**. Entrambe le attività Gestione dominio e Individuazione informazioni saranno disponibili. Verrà di nuovo visualizzata la home page.  
  
    -   **Annulla-rimane nella schermata corrente**: la finestra popup verrà chiusa e verrà visualizzata nuovamente la schermata di gestione del dominio.  
  
8.  Fare clic su **Chiudi** per salvare il lavoro e tornare alla home page di DQS. Nello stato della Knowledge Base verrà visualizzata la stringa "Criteri di corrispondenza -" e lo stato corrente. Se si è fatto clic su **Chiudi** dalla schermata **Risultati corrispondenza** , nello stato verrà visualizzata la stringa seguente: "Criteri di corrispondenza - Risultati". Se si è fatto clic su Chiudi dalla schermata **Criteri di corrispondenza**, nello stato verrà visualizzata la stringa seguente: "Criteri di corrispondenza - Criteri di corrispondenza". Dopo avere fatto clic su **Chiudi**per eseguire l'attività **Individuazione informazioni** è necessario tornare all'attività **Criteri di corrispondenza** ; fare clic su **Fine**, quindi su **Sì** per pubblicare la Knowledge Base o su **No** per salvare il lavoro nella Knowledge Base e uscire.  
  
    > [!NOTE]  
    >  Clic su **Chiudi** mentre un processo di corrispondenza è in esecuzione, tale processo non verrà interrotto quando si fa clic su **Chiudi**. È possibile riaprire la Knowledge Base e verificare che il processo sia ancora in esecuzione oppure, se completato, che ne vengano visualizzati i risultati. Se il processo non è stato completato, lo stato di avanzamento verrà visualizzato sullo schermo.  
  
9. Fare clic su **Annulla** per interrompere l'attività relativa ai criteri di corrispondenza. Il lavorò verrà perso e verrà visualizzata di nuovo la home page di DQS.  
  
##  <a name="FollowUp"></a>Completamento: fasi successive alla creazione dei criteri di corrispondenza  
 Dopo avere creato dei criteri di corrispondenza, è possibile eseguire un progetto di corrispondenza basato sulla Knowledge Base contenente i criteri. Per altre informazioni, vedere [Eseguire un progetto corrispondente](../../2014/data-quality-services/run-a-matching-project.md).  
  
##  <a name="Tabs"></a>Schede Profiler e risultati  
 Le schede Profiler e Risultati contengono statistiche per la pagina Criteri di corrispondenza e per la pagina Risultati corrispondenza.  
  
###  <a name="Profiler"></a>Scheda Profiler  
 Fare clic sulla scheda **Profiler** per visualizzare statistiche per il database di origine e per ogni campo incluso nella regola dei criteri. Le statistiche verranno aggiornate all'esecuzione della regola dei criteri.  
  
 Per ulteriori informazioni sull'interpretazione delle statistiche seguenti, vedere [Modalità di impostazione dei parametri relativi alle regole di corrispondenza](#MatchingRules).  
  
 Le statistiche relative al database di origine includono:  
  
-   **Record**: numero totale di record nel database di origine  
  
-   **Valori totali**: numero totale di valori nei campi dell'origine dati  
  
-   **Nuovi valori**: numero totale di valori nuovi dall'esecuzione precedente e relativa percentuale dell'intero  
  
-   **Valori univoci**: numero totale di valori univoci nei campi e relativa percentuale dell'intero  
  
-   **Nuovi valori univoci**: numero totale di valori univoci nuovi nei campi e relativa percentuale dell'intero  
  
 Le statistiche relative ai campi includono:  
  
-   **Nome campo**  
  
-   **Nome di dominio**  
  
-   **Nuovo**: numero di nuovi valori e percentuale di nuovi valori rispetto ai valori esistenti nel dominio  
  
-   **Unique**: numero di record univoci nel campo e relativa percentuale del totale  
  
-   **Completezza**: la completezza di ogni campo di origine di cui è stato eseguito il mapping per l'esercizio corrispondente  
  
###  <a name="Notifications"></a>Notifiche dei criteri di corrispondenza  
 Per l'attività relativa ai criteri di corrispondenza, le condizioni seguenti generano notifiche:  
  
-   Il campo è vuoto in tutti i record; è consigliabile eliminarlo dal mapping.  
  
-   Il punteggio di completezza del campo è molto basso; è consigliabile eliminarlo dal mapping.  
  
-   Un campo contiene solo valori non validi; è necessario verificare il mapping e la rilevanza delle regole di dominio sul contenuto del campo.  
  
-   Un campo contiene un basso livello di valori validi; è necessario verificare il mapping e la rilevanza delle regole di dominio sul contenuto del campo.  
  
-   Vi è un livello elevato di unicità nel campo. L'utilizzo del campo nei criteri di corrispondenza può diminuire i risultati di corrispondenza.  
  
###  <a name="ResultsTab"></a>Scheda Risultati corrispondenza  
 Fare clic sulla scheda **Risultati corrispondenza** per visualizzare statistiche relative all'esecuzione della regola dei criteri di corrispondenza e all'esecuzione della regola precedente. Se è stata eseguita la stessa regola più di una volta con i parametri diversi, nella tabella dei risultati di corrispondenza verranno visualizzate statistiche per entrambe le esecuzioni, consentendone il confronto. È inoltre possibile ripristinare la regola precedente, se necessario.  
  
 Le statistiche includono gli elementi seguenti:  
  
-   Numero complessivo di record nel database  
  
-   Numero complessivo di record corrispondenti nel database  
  
-   Numero di record nel database che non si considerano duplicati  
  
-   Numero di cluster individuati  
  
-   Dimensione media di un cluster (numero di record duplicati diviso numero di cluster)  
  
-   Il minor numero di duplicati in un cluster  
  
-   Il maggior numero di duplicati in un cluster  
  
  
