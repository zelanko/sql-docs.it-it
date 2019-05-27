---
title: Traccia (Client di Data Mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tracer
- connections
ms.assetid: 4aea3e17-cd0f-48dd-8f22-b54a6c716426
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 576cb395f7f488eec8ebf28ab5bc7f226cb81809
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065888"
---
# <a name="trace-data-mining-client-for-excel"></a>Traccia (client di data mining per Excel)
  ![Pulsante traccia](media/misc-trace.gif "pulsante traccia")  
  
 Il **Tracer** finestra di dialogo consente di monitorare le istruzioni vengono inviate all'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che si usa per il data mining. Dopo aver creato una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], tutte le interazioni tra il client e server vengono registrate nel **traccia** riquadro, incluse le istruzioni creano strutture, aggiungere modelli di data mining e rendano le stime, nonché alcuni messaggi restituiti dal server.  
  
 A seconda dell'azione richiesta, l'istruzione potrebbe essere una query di modifica o di definizione dati DMX (Data Mining Extensions), un pacchetto ASSL (Analysis Services Scripting Language) o una chiamata a una stored procedure di Analysis Services. Non vengono tuttavia visualizzati i risultati numerici e i valori dei dati effettivi.  
  
 **Traccia** monitora solo la connessione corrente e il contenuto del **traccia** non vengono archiviate nella finestra di dialogo.  
  
## <a name="options"></a>Opzioni  
 Riquadro Utilità di traccia  
 Vengono elencate tutte le istruzioni inviate dal client di Excel al server.  
  
 A seconda dell'azione richiesta, l'istruzione potrebbe essere una modifica dei dati DMX o un'istruzione per la definizione dei dati, una chiamata a una stored procedure di Analysis Services o un pacchetto XML/A.  
  
 **Connessione corrente**  
 Fare clic per visualizzare la definizione della connessione corrente. La definizione include il nome della connessione, il provider, l'origine dati e il catalogo, l'ora dell'ultimo utilizzo della connessione per una transazione e lo stato corrente, ovvero aperta o inattiva.  
  
 **Usa modelli di sessione**  
 Selezionare questa casella di controllo per archiviare i modelli e le strutture di data mining come oggetti temporanei nel server. Le strutture o i modelli creati saranno disponibili solo per la durata della connessione corrente.  
  
 Deselezionare questa opzione per salvare i modelli o le strutture archiviandoli in un server Analysis Services.  
  
 **Nota** la possibilità di utilizzare oggetti temporanei è disponibile solo quando si utilizza strumenti di analisi tabelle per Excel. I componenti Modelli di data mining per Visio e Client di data mining per Excel richiedono l'archiviazione delle strutture e dei modelli nel server.  
  
## <a name="tracing-temporary-structures-and-models"></a>Traccia di strutture e modelli temporanei  
 Se si utilizza il componente Strumenti di analisi tabelle, tramite il quale vengono creati, per impostazione predefinita, strutture e modelli temporanei, l'attività tra il server e il client viene monitorata, ma le strutture o i modelli creati non vengono salvati in modo permanente nel server.  
  
 Se si desidera conservare il lavoro quando si usa uno degli strumenti di analisi tabelle, è possibile deselezionare l'opzione **Usa modelli di sessione**, in modo che i modelli essere salvato in modo permanente nel server. È inoltre possibile copiare le istruzioni nel **traccia** riquadro in un file in modo che sia possibile ricreare il lavoro in un secondo momento.  
  
## <a name="understanding-sessions"></a>Informazioni sulle sessioni  
 Quando ci si connette a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], il componente aggiuntivo di data mining crea una sessione. A ogni sessione viene assegnato un identificatore che contraddistingue una sessione esistente nell'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. L'identificatore di sessione non rappresenta tuttavia una garanzia di validità della sessione. La sessione può infatti scadere in caso di timeout o se la connessione associata alla sessione viene interrotta. Se la sessione scade e non è più valida, la sessione viene terminata da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e viene eseguito il rollback di eventuali transazioni in corso. Se viene inviato un messaggio con un identificatore di sessione non più valido, l'operazione non riesce e viene generato un errore per segnalare che non è possibile trovare la sessione specificata.  
  
 Sebbene alcuni modelli di data mining siano archiviati in modo esplicito nel server, i modelli e delle strutture di data mining di sessione non vengono archiviati e non viene mantenuta nessuna registrazione relativa all'attività di data mining di sessione. Poiché i modelli e le strutture di data mining temporanei vengono eliminati non appena si termina la sessione, è consigliabile evitare di chiudere la cartella di lavoro di Excel in uso senza prima aver salvato i dati che si desidera mantenere.  
  
## <a name="changing-connections"></a>Cambio di connessioni  
 Se si cambia connessione, le tracce delle connessioni precedenti non vengono eliminate. La sessione viene cancellata solo in seguito alla chiusura della cartella di lavoro.  
  
 Se si cambia connessione mentre si lavora in una cartella di lavoro di Excel, la modifica delle connessioni non viene registrata nel **traccia** riquadro. Per visualizzare in modo esplicito il nome e lo stato della connessione corrente, è necessario fare clic su **connessione corrente**.  
  
## <a name="understanding-statements-in-the-tracer"></a>Informazioni sulle istruzioni visualizzate nel riquadro DMTracer  
 DMX (Data Mining Extensions) è un linguaggio che è possibile utilizzare per creare e utilizzare modelli di data mining in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Tramite DMX è possibile creare la struttura dei nuovi modelli di data mining, eseguire il training dei modelli, nonché esplorarli, gestirli ed eseguire stime basate su di essi. DMX comprende istruzioni DDL (Data Definition Language) e DML (Data Manipulation Language), nonché funzioni e operatori.  
  
 Una discussione completa sulle istruzioni DMX e la relativa sintassi esula dagli scopi di questo argomento. Tuttavia, è possibile usare le informazioni contenute nel **traccia** riquadro che contiene informazioni dettagliate sul comportamento di un'istruzione DMX. I componenti aggiuntivi Data mining per Excel consentono inoltre di compilare istruzioni DMX complesse e di interagire con un server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per altre informazioni, vedere [Query &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](query-sql-server-data-mining-add-ins.md).  
  
> [!NOTE]  
>  In numerose istruzioni DMX vengono utilizzati parametri. Per i tipi semplici, i valori dei parametri vengono elencati sotto l'istruzione. Per i tipi complessi, tuttavia, viene elencato solo il tipo del parametro.  
  
 In SQL Server Analysis Services viene inoltre utilizzato il protocollo XMLA (XML for Analysis) per gestire tutte le comunicazioni tra le applicazioni client, inclusi Client di data mining per Excel e un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Per ulteriori informazioni sulla sintassi DMX e sui comandi e sugli elementi in XMLA, vedere la documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Alcune istruzioni inviate al server possono includere query che chiamano stored procedure di sistema di Analysis Services. Per ulteriori informazioni, vedere la documentazione online di SQL Server.  
  
  
