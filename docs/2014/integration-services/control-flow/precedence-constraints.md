---
title: Vincoli di precedenza | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- control flow [Integration Services], precedence constraints
- precedence constraints [Integration Services]
- constraints [Integration Services]
- sequence execution options [Integration Services]
- containers [Integration Services], precedence constraints
ms.assetid: c5ce5435-fd89-4156-a11f-68470a69aa9f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bc23747a13ee2e5b126b7e57ba7121878d05643d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176471"
---
# <a name="precedence-constraints"></a>Vincoli di precedenza
  I vincoli di precedenza collegano eseguibili, contenitori e attività di pacchetti in modo da formare un flusso di controllo e specificano le condizioni che determinano se tali eseguibili devono essere eseguiti. Un eseguibile può essere costituito da un gestore di evento o da un contenitore Ciclo For, Ciclo Foreach o Sequenza. Anche nei gestori di eventi vengono utilizzati vincoli di precedenza per collegare gli eseguibili in modo da formare un flusso di controllo.

 Un vincolo di precedenza collega due eseguibili: l'eseguibile con precedenza e l'eseguibile soggetto al vincolo. L'eseguibile con precedenza viene eseguito prima dell'eseguibile soggetto al vincolo e il risultato della sua esecuzione può determinare se l'eseguibile soggetto al vincolo verrà eseguito o meno. Nella figura seguente vengono illustrati due eseguibili collegati da vincoli di precedenza.

 ![Eseguibili collegati con un vincolo di precedenza](../media/ssis-pcsimple.gif "Eseguibili collegati con un vincolo di precedenza")

 In un flusso di controllo lineare, ovvero senza diramazioni, la sequenza di esecuzione delle attività è regolata unicamente dai vincoli di precedenza. In un flusso di controllo con diramazioni l'ordine di esecuzione delle attività e dei contenitori situati immediatamente dopo una diramazione è determinato dal motore di run-time di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . Il motore di run-time determina anche l'ordine di esecuzione dei flussi di lavoro non connessi in un flusso di controllo.

 L'architettura a contenitori nidificati di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] consente a tutti i contenitori, ad eccezione del contenitore Host attività che incapsula una sola attività, di includere altri contenitori, ognuno con un proprio flusso di controllo. I contenitori Ciclo For, Ciclo Foreach e Sequenza possono includere più attività e altri contenitori, che a loro volta possono includere più attività e contenitori. Un pacchetto con un'attività Script e un contenitore Sequenza può ad esempio includere un vincolo di precedenza che collega l'attività Script e il contenitore Sequenza. Il contenitore Sequenza include tre attività Script e i relativi vincoli di precedenza collegano le tre attività Script in modo da formare un flusso di controllo. Nella figura seguente vengono illustrati i vincoli di precedenza utilizzati in un pacchetto con due livelli di nidificazione.

 ![Vincoli di precedenza in un pacchetto](../media/mw-dts-12.gif "Vincoli di precedenza in un pacchetto")

 Poiché il pacchetto è al livello principale della gerarchia dei contenitori di [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , non è possibile collegare più pacchetti tramite vincoli di precedenza. È tuttavia possibile aggiungere un'attività Esegui pacchetto a un pacchetto e in tal modo collegare indirettamente un altro pacchetto al flusso di controllo.

 Per configurare i vincoli di precedenza, procedere nel modo seguente:

-   Specificare un'operazione di valutazione. Il vincolo di precedenza utilizza un valore di vincolo, un'espressione o entrambi o per determinare se l'eseguibile deve essere eseguito o meno.

-   Se il vincolo di precedenza utilizza il risultato di un'esecuzione, sarà possibile specificare se l'esecuzione deve avere esito positivo, negativo o essere semplicemente completata.

-   Se il vincolo di precedenza utilizza il risultato di una valutazione, sarà possibile specificare un'espressione che restituisce un valore booleano.

-   Specificare se il vincolo di precedenza deve essere valutato singolarmente o insieme ad altri vincoli applicati all'eseguibile soggetto al vincolo.

## <a name="evaluation-operations"></a>Operazioni di valutazione
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] offre le operazioni di valutazione seguenti:

-   Un vincolo che utilizza solo il risultato dell'esecuzione dell'eseguibile con precedenza per determinare se l'eseguibile soggetto al vincolo deve essere eseguito o meno. Il risultato dell'esecuzione dell'eseguibile con precedenza indica se l'esecuzione ha avuto esito positivo, negativo o semplicemente se è stata completata. Si tratta dell'operazione predefinita.

-   Un'espressione che viene valutata per determinare se l'eseguibile soggetto al vincolo deve essere eseguito o meno. Se l'espressione restituisce True, l'eseguibile soggetto al vincolo verrà eseguito.

-   Un'espressione e un vincolo che combinano i requisiti del risultato dell'esecuzione dell'eseguibile con precedenza e del risultato restituito dalla valutazione dell'espressione.

-   Un'espressione o un vincolo che utilizza il risultato dell'esecuzione dell'eseguibile con precedenza o il risultato restituito dalla valutazione dell'espressione.

 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] In Progettazione SSIS vengono usati i colori per identificare il tipo di vincolo di precedenza. Il vincolo Success è verde, il vincolo Failure è rosso e il vincolo Completion è blu. Per visualizzare in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] etichette di testo che indicano il tipo di vincolo, è necessario configurare le funzionalità di accessibilità di Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .

 L'espressione deve essere un'espressione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] valida e in essa possono essere incluse funzioni, operatori, nonché variabili personalizzate e di sistema. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md) e [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md).

## <a name="execution-results"></a>Risultati di esecuzione
 I vincoli di precedenza possono utilizzare i risultati di esecuzione seguenti, singolarmente o in combinazione con un'espressione.

-   Il vincolo Completion richiede solo che l'eseguibile con precedenza abbia completato l'esecuzione, indipendentemente dall'esito, affinché l'eseguibile soggetto al vincolo venga eseguito.

-   Il vincolo Success richiede che l'eseguibile con precedenza abbia completato correttamente l'esecuzione, affinché l'eseguibile soggetto al vincolo venga eseguito.

-   Il vincolo Failure richiede che l'eseguibile con precedenza non abbia completato correttamente l'esecuzione, affinché l'eseguibile soggetto al vincolo venga eseguito.

> [!NOTE]
>  È possibile raggruppare in una condizione con AND logico solo vincoli di precedenza appartenenti alla stessa raccolta `Precedence Constraint`. Non è ad esempio possibile combinare i vincoli di precedenza utilizzati in due contenitori Ciclo Foreach diversi.

## <a name="configuration-of-the-precedence-constraint"></a>Configurazione del vincolo di precedenza
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.

 Per informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , vedere [Editor vincoli di precedenza](../precedence-constraint-editor.md).

 Per informazioni sull'impostazione di queste proprietà a livello di codice, vedere <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>.

## <a name="related-tasks"></a>Attività correlate
 Per informazioni dettagliate sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:

-   [Impostazione delle proprietà di un vincolo di precedenza](../set-the-properties-of-a-precedence-constraint.md)

-   [Impostazione del valore di un vincolo di precedenza tramite il menu di scelta rapida](../set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)

-   [Connessione di attività e contenitori tramite un vincolo di precedenza predefinito](../connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)

     In questo argomento sono fornite informazioni sulla modalità di impostazione del comportamento predefinito dei vincoli di precedenza e sulla modalità di connessione di file eseguibili tramite i vincoli di precedenza predefiniti.

## <a name="related-content"></a>Contenuto correlato
 Articolo tecnico relativo agli [esempi di espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=220761)nel sito Web social.technet.microsoft.com

## <a name="see-also"></a>Vedere anche
 [Aggiungere espressioni ai vincoli di precedenza](../add-expressions-to-precedence-constraints.md) [più vincoli di precedenza](../multiple-precedence-constraints.md)


