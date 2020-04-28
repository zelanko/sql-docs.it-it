---
title: Trace (client di data mining per Excel) | Microsoft Docs
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
ms.openlocfilehash: 19a30107af159c1cd87324290844172371f02752
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175570"
---
# <a name="trace-data-mining-client-for-excel"></a>Traccia (client di data mining per Excel)
  ![Pulsante Traccia](media/misc-trace.gif "Pulsante Traccia")

 La finestra di dialogo **traccia** consente di monitorare le istruzioni inviate all'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizzata per data mining. Dopo aver creato una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], tutte le interazioni tra il client e il server vengono registrate nel riquadro di analisi, incluse le istruzioni che consentono di creare strutture, aggiungere modelli di data mining ed eseguire stime, nonché alcuni messaggi restituiti dal server. **Tracer**

 A seconda dell'azione richiesta, l'istruzione potrebbe essere una query di modifica o di definizione dati DMX (Data Mining Extensions), un pacchetto ASSL (Analysis Services Scripting Language) o una chiamata a una stored procedure di Analysis Services. Non vengono tuttavia visualizzati i risultati numerici e i valori dei dati effettivi.

 **Trace** monitora solo la connessione corrente e il contenuto della finestra di dialogo di **traccia** non viene archiviato.

## <a name="options"></a>Opzioni
 Riquadro di traccia elenca tutte le istruzioni inviate dal client di Excel al server.

 A seconda dell'azione richiesta, l'istruzione potrebbe essere una modifica dei dati DMX o un'istruzione per la definizione dei dati, una chiamata a una stored procedure di Analysis Services o un pacchetto XML/A.

 **Connessione corrente** Fare clic su questo pulsante per visualizzare la definizione della connessione corrente. La definizione include il nome della connessione, il provider, l'origine dati e il catalogo, l'ora dell'ultimo utilizzo della connessione per una transazione e lo stato corrente, ovvero aperta o inattiva.

 **Usare i modelli di sessione** Selezionare questa casella di controllo per archiviare i modelli e le strutture data mining come oggetti temporanei sul server. Le strutture o i modelli creati saranno disponibili solo per la durata della connessione corrente.

 Deselezionare questa opzione per salvare i modelli o le strutture archiviandoli in un server Analysis Services.

 **Nota** La possibilità di utilizzare oggetti temporanei è disponibile solo quando si utilizzano gli strumenti di analisi tabelle per Excel. I componenti Modelli di data mining per Visio e Client di data mining per Excel richiedono l'archiviazione delle strutture e dei modelli nel server.

## <a name="tracing-temporary-structures-and-models"></a>Traccia di strutture e modelli temporanei
 Se si utilizza il componente Strumenti di analisi tabelle, tramite il quale vengono creati, per impostazione predefinita, strutture e modelli temporanei, l'attività tra il server e il client viene monitorata, ma le strutture o i modelli creati non vengono salvati in modo permanente nel server.

 Se si desidera mantenere il lavoro quando si utilizza uno degli strumenti di analisi tabelle, è possibile deselezionare l'opzione **Usa modelli di sessione**per fare in modo che i modelli vengano salvati in modo permanente nel server. È anche possibile copiare le istruzioni nel riquadro di **traccia** in un file in modo da poter ricreare il lavoro in un secondo momento.

## <a name="understanding-sessions"></a>Informazioni sulle sessioni
 Quando ci si connette a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], il componente aggiuntivo di data mining crea una sessione. A ogni sessione viene assegnato un identificatore che contraddistingue una sessione esistente nell'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. L'identificatore di sessione non rappresenta tuttavia una garanzia di validità della sessione. La sessione può infatti scadere in caso di timeout o se la connessione associata alla sessione viene interrotta. Se la sessione scade e non è più valida, la sessione viene terminata da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e viene eseguito il rollback di eventuali transazioni in corso. Se viene inviato un messaggio con un identificatore di sessione non più valido, l'operazione non riesce e viene generato un errore per segnalare che non è possibile trovare la sessione specificata.

 Sebbene alcuni modelli di data mining siano archiviati in modo esplicito nel server, i modelli e delle strutture di data mining di sessione non vengono archiviati e non viene mantenuta nessuna registrazione relativa all'attività di data mining di sessione. Poiché i modelli e le strutture di data mining temporanei vengono eliminati non appena si termina la sessione, è consigliabile evitare di chiudere la cartella di lavoro di Excel in uso senza prima aver salvato i dati che si desidera mantenere.

## <a name="changing-connections"></a>Cambio di connessioni
 Se si cambia connessione, le tracce delle connessioni precedenti non vengono eliminate. La sessione viene cancellata solo in seguito alla chiusura della cartella di lavoro.

 Se si modificano le connessioni durante l'utilizzo di una cartella di lavoro di Excel, la modifica delle connessioni non viene registrata nel riquadro di **traccia** . Per visualizzare in modo esplicito il nome e lo stato della connessione corrente, è necessario fare clic su **connessione corrente**.

## <a name="understanding-statements-in-the-tracer"></a>Informazioni sulle istruzioni visualizzate nel riquadro DMTracer
 DMX (Data Mining Extensions) è un linguaggio che è possibile utilizzare per creare e utilizzare modelli di data mining in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Tramite DMX è possibile creare la struttura dei nuovi modelli di data mining, eseguire il training dei modelli, nonché esplorarli, gestirli ed eseguire stime basate su di essi. DMX comprende istruzioni DDL (Data Definition Language) e DML (Data Manipulation Language), nonché funzioni e operatori.

 Una discussione completa sulle istruzioni DMX e la relativa sintassi esula dagli scopi di questo argomento. Tuttavia, è possibile utilizzare le informazioni nel riquadro di **traccia** per trovare informazioni dettagliate sul comportamento di un'istruzione DMX. I componenti aggiuntivi Data mining per Excel consentono inoltre di compilare istruzioni DMX complesse e di interagire con un server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per ulteriori informazioni, vedere [Query &#40;SQL Server componenti aggiuntivi Data Mining&#41;](query-sql-server-data-mining-add-ins.md).

> [!NOTE]
>  In numerose istruzioni DMX vengono utilizzati parametri. Per i tipi semplici, i valori dei parametri vengono elencati sotto l'istruzione. Per i tipi complessi, tuttavia, viene elencato solo il tipo del parametro.

 In SQL Server Analysis Services viene inoltre utilizzato il protocollo XMLA (XML for Analysis) per gestire tutte le comunicazioni tra le applicazioni client, inclusi Client di data mining per Excel e un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].

 Per ulteriori informazioni sulla sintassi DMX e sui comandi e sugli elementi in XMLA, vedere la documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

 Alcune istruzioni inviate al server possono includere query che chiamano stored procedure di sistema di Analysis Services. Per ulteriori informazioni, vedere la documentazione online di SQL Server.


