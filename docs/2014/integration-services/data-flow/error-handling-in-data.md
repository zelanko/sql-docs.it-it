---
title: Gestione degli errori nei dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data conversion errors [Integration Services]
- errors [Integration Services], data flow components
- lookups [Integration Services]
- errors [Integration Services]
- errors [Integration Services], data flow outputs
- error outputs [Integration Services]
- data flow [Integration Services], errors
- expressions [Integration Services], errors
ms.assetid: c61667b4-25cb-4d45-a52f-a733e32863f4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b5a98877e04a077bf1bb1c0c527500f3102b862
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378567"
---
# <a name="error-handling-in-data"></a>Gestione degli errori nei dati
  Quando tramite un componente flusso di dati viene applicata una trasformazione ai dati delle colonne, vengono estratti dati dalle origini o vengono caricati dati nelle destinazioni, possono verificarsi errori. Gli errori sono spesso dovuti alla presenza di valori non previsti. Una conversione di dati può ad esempio avere esito negativo perché una colonna contiene una stringa anziché un numero, un inserimento in una colonna di database può avere esito negativo perché i dati rappresentano una data mentre la colonna ha un tipo di dati numeric oppure la valutazione di un'espressione può avere esito negativo perché il valore di una colonna è zero e dà luogo a un'operazione matematica non valida.  
  
 Gli errori rientrano in genere nelle categorie seguenti:  
  
-   Errori di conversione dei dati, che si verificano se una conversione comporta la perdita di cifre significative o non significative oppure il troncamento di una stringa. Gli errori di conversione dei dati si verificano anche quando la conversione richiesta non è supportata.  
  
-   Errori di valutazione delle espressioni, che si verificano se le espressioni che vengono valutate in fase di esecuzione eseguono operazioni non valide o non risultano sintatticamente corrette a causa di valori mancanti o errati.  
  
-   Errori di ricerca, che si verificano se un'operazione di ricerca non trova una corrispondenza nella tabella di ricerca.  
  
 Molti componenti dei flussi di dati supportano output degli errori che consentono di controllare la modalità di gestione degli errori a livello di riga nei dati in ingresso e in uscita. È possibile specificare il comportamento che dovrà avere il componente in caso di troncamento o errore impostando opzioni sulle singole colonne di input o di output. È ad esempio possibile specificare che il componente dovrà generare un errore se il nome di un cliente viene troncato, mentre gli errori relativi ad altre colonne contenenti dati meno importanti potranno essere ignorati.  
  
 L'output degli errori può essere connesso all'input di un'altra trasformazione o caricato in una destinazione diversa da quella dell'output non degli errori. L'output degli errori può ad esempio essere connesso a una trasformazione Colonna derivata che fornisce una stringa per una colonna vuota.  
  
 Nella figura seguente viene illustrato un semplice flusso di dati che include un output degli errori.  
  
 ![Flusso di dati con output degli errori](../media/mw-dts-11.gif "Flusso di dati con output degli errori")  
  
 Oltre alle colonne di dati, l'output degli errori include anche le colonne **ErrorCode** ed **ErrorColumn** . La colonna **ErrorCode** identifica l'errore, mentre la colonna **ErrorColumn** contiene l'identificatore di derivazione della colonna degli errori. Per visualizzare i metadati di queste colonne, fare clic sul percorso che connette l'output degli errori al componente successivo nel flusso di dati. In alcune circostanze il valore della colonna **ErrorColumn** è impostato su zero. Questa situazione si verifica quando la condizione di errore interessa l'intera riga anziché una singola colonna, ad esempio quando nella trasformazione Ricerca una ricerca non riesce.  
  
 Per altre informazioni, vedere [Flusso di dati](data-flow.md) e [Percorsi in Integration Services](integration-services-paths.md).  
  
 Per un elenco di errori, avvisi e altri messaggi di Integration Services, vedere [Guida di riferimento ai messaggi e agli errori di Integration Services](../integration-services-error-and-message-reference.md).  
  
## <a name="error-and-truncation-options"></a>Opzioni relative a errori e troncamenti  
 Gli errori possono essere suddivisi in due categorie: errori o troncamenti. Un errore indica un problema certo e genera un risultato NULL. Rientrano in questa categoria ad esempio gli errori di conversione dei dati e gli errori di valutazione delle espressioni. Un errore può essere ad esempio causato dal tentativo di convertire in un numero una stringa che contiene caratteri alfabetici. Le conversioni di dati, le valutazioni delle espressioni e le assegnazioni dei risultati delle espressioni a variabili, proprietà e colonne di dati può avere esito negativo a causa di cast non validi o tipi di dati non compatibili. Per altre informazioni, vedere [Cast &#40;espressione SSIS&#41;](../expressions/cast-ssis-expression.md), [Tipi di dati nelle espressioni di Integration Services](../expressions/integration-services-data-types-in-expressions.md) e [Tipi di dati di Integration Services](integration-services-data-types.md).  
  
 Un troncamento è meno grave di un errore. Il troncamento genera risultati che possono essere utilizzabili se non addirittura utili. Si può scegliere se considerare i troncamenti come errori o come condizioni accettabili. Se ad esempio si inserisce una stringa di 15 caratteri in una colonna con larghezza di un carattere, si può scegliere di troncare la stringa.  
  
 È possibile configurare la modalità di gestione di errori e troncamenti utilizzata da origini, trasformazioni e destinazioni. Nella tabella seguente vengono descritte le opzioni disponibili.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Interrompi componente|Quando si verifica un errore o un troncamento l'attività Flusso di dati viene interrotta. Questa è l'opzione predefinita per errori e troncamenti.|  
|Ignora errore|L'errore o il troncamento viene ignorato e la riga di dati viene indirizzata all'output della trasformazione o dell'origine.|  
|Reindirizza riga|La riga di dati contenente l'errore o il troncamento viene inviata all'output degli errori dell'origine, della trasformazione o della destinazione.|  
  
## <a name="adding-the-error-description"></a>Aggiunta della descrizione dell'errore  
 Per impostazione predefinita l'output egli errori include il codice numerico dell'errore e contiene in genere l'identificatore della colonna in cui si è verificato l'errore. È possibile utilizzare il componente script per includere la descrizione dell'errore in una colonna aggiuntiva, utilizzando una singola riga di script per chiamare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> dell'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.  
  
 Il componente script può essere aggiunto al segmento del flusso di dati relativo agli errori, in qualsiasi punto a valle dei componenti del flusso di dati di cui si desidera acquisire gli errori, ma viene in genere collocato immediatamente prima della scrittura delle righe di errore in una destinazione. In questo modo, lo script cerca solo le descrizioni relative alle righe di errore da scrivere. Se ad esempio il segmento del flusso di dati relativo agli errori corregge alcuni errori, le relative righe di errore non verranno scritte in una destinazione degli errori. Per altre informazioni, vedere [ottimizzazione un Output degli errori con il componente Script](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md).  
  
### <a name="to-configure-an-error-output"></a>Per configurare un output degli errori  
  
-   [Configurazione di un output degli errori in un componente del flusso di dati](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](data-flow.md)   
 [Trasformazione di dati con le trasformazioni](transformations/transform-data-with-transformations.md)   
 [Connessione di componenti con i percorsi](../connect-components-with-paths.md)   
 [Attività Flusso di dati](../control-flow/data-flow-task.md)   
 [Flusso di dati](data-flow.md)  
  
  
