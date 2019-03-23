---
title: Trasformazione Ricerca termini | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termlookuptrans.f1
helpviewer_keywords:
- extracting data [Integration Services]
- match extracted terms [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- lookups [Integration Services]
- counting extracted items
- Term Lookup transformation
ms.assetid: 3c0fa2f8-cb6a-4371-b184-7447be001de1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 01b6388dbec5ed563dd8e7fa4476335a3ace998d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380569"
---
# <a name="term-lookup-transformation"></a>Ricerca termini - trasformazione
  La trasformazione Ricerca termini rileva le corrispondenze tra i termini estratti dal testo in una colonna di input della trasformazione e quelli contenuti in una tabella di riferimento, quindi conta il numero delle occorrenze di un termine della tabella di ricerca nel set di dati di input e scrive tale numero nelle colonne di output della trasformazione, insieme al termine della tabella di riferimento. Questa trasformazione può essere utilizzata per creare un elenco di termini personalizzato basato sul testo di input, completo di statistiche sulla frequenza dei termini.  
  
 Prima di eseguire una ricerca la trasformazione Ricerca termini estrae le parole dal testo di una colonna di input utilizzando lo stesso procedimento utilizzato dalla trasformazione Estrazione termini:  
  
-   Il testo viene suddiviso in frasi.  
  
-   Le frasi vengono suddivise in parole.  
  
-   Le parole vengono normalizzate.  
  
 Per personalizzare ulteriormente la determinazione delle corrispondenze, è possibile configurare la trasformazione Ricerca termini in modo da fare distinzione tra maiuscole e minuscole.  
  
## <a name="matches"></a>Corrisponde a  
 La trasformazione Ricerca termini esegue una ricerca e restituisce un valore utilizzando le regole seguenti:  
  
-   Se la trasformazione è configurata in modo da fare distinzione tra maiuscole e minuscole, i termini che presentano combinazioni di maiuscole e minuscole non corrispondenti vengono ignorati. I termini *studente* e *STUDENTE* , ad esempio, vengono considerati come due parole diverse.  
  
    > [!NOTE]  
    >  Una parola priva di maiuscole può corrispondere a una parola con iniziale maiuscola all'inizio di una frase. Le parole *studente* e *Studente* , ad esempio, vengono considerate corrispondenti quando *Studente* è la prima parola di una frase.  
  
-   Se nella tabella di riferimento è presente la forma plurale del sostantivo o sintagma nominale, la ricerca individuerà solo la forma plurale del sostantivo o sintagma nominale. Tutte le istanze della parola *studenti* , ad esempio, vengono conteggiate separatamente da quelle della parola *studente*.  
  
-   Se nella tabella di riferimento è presente solo la forma singolare della parola, sia la forma singolare che quella plurale della parola o frase verranno considerate corrispondenti alla forma singolare. Se ad esempio la tabella di ricerca contiene la parola *studente*e la trasformazione trova *studente* e *studenti*, entrambe le parole verranno conteggiate come corrispondenze del termine di ricerca *studente*.  
  
-   Se il testo nella colonna di input è un sintagma nominale lemmatizzato, la normalizzazione interesserà solo l'ultima parola del sintagma nominale. La versione lemmatizzata di *doctors appointments* è ad esempio *doctors appointment*.  
  
 Quando un elemento di ricerca contiene termini che si sovrappongono nel set di riferimento, ovvero viene trovato un termine secondario in più di un record di riferimento, la trasformazione Ricerca termini restituisce solo un risultato della ricerca. Nell'esempio seguente viene illustrato il risultato ottenuto quando un elemento di ricerca contiene un termine secondario sovrapposto. Il termine secondario sovrapposto in questo caso è *Windows*, presente in due termini di riferimento. La trasformazione non restituisce tuttavia due risultati ma solo un termine di riferimento, ovvero *Windows*. Il secondo termine di riferimento, *Windows 7 Professional*, non viene restituito.  
  
|Elemento|Value|  
|----------|-----------|  
|Termine di input|Windows 7 Professional|  
|Termini di riferimento|Windows 7 x64 Professional|  
|Output|Windows|  
  
 La trasformazione Ricerca termini può trovare anche sostantivi e sintagmi nominali contenenti caratteri speciali che possono essere presenti anche nei dati della tabella di riferimento. I caratteri speciali sono i seguenti: %, @, &, $, #, \*, :, ;, ., **,**, !, ?, \<, >, +, =, ^, ~, |, \\, /, (, ), [, ], {, }, " e '.  
  
## <a name="data-types"></a>Tipi di dati  
 La trasformazione Ricerca termini può utilizzare solo colonne con tipo di dati DT_WSTR o DT_NTEXT. Se una colonna contiene testo ma non ha uno di questi tipi di dati, sarà possibile utilizzare la trasformazione Conversione dati per aggiungere al flusso di dati una colonna con tipo di dati DT_WSTR o DT_NTEXT e copiare nella nuova colonna i valori della colonna originale. L'output della trasformazione Conversione dati può essere quindi utilizzato come input della trasformazione Ricerca termini. Per altre informazioni, vedere [Trasformazione Conversione dati](data-conversion-transformation.md).  
  
## <a name="configuration-the-term-lookup-transformation"></a>Configurazione della trasformazione Ricerca termini  
 Le colonne di input della trasformazione Ricerca termini includono la proprietà InputColumnType che ne indica l'uso. InputColumnType può contenere i valori seguenti:  
  
-   Il valore 0 indica che la colonna viene semplicemente passata all'output e non viene utilizzata nella ricerca.  
  
-   Il valore 1 indica che la colonna viene utilizzata solo nella ricerca.  
  
-   Il valore 2 indica che la colonna viene passata all'output e utilizzata anche nella ricerca.  
  
 Le colonne di output della trasformazione la cui proprietà InputColumnType è impostata su 0 o 2 includono la proprietà CustomLineageID, che contiene l'identificatore di derivazione assegnato alla colonna da un componente a monte nel flusso di dati.  
  
 La trasformazione Ricerca termini aggiunge all'output della trasformazione due colonne, che per impostazione predefinita sono denominate `Term` e `Frequency`. `Term` contiene un termine della tabella di ricerca, mentre la colonna `Frequency` contiene il numero di occorrenze di tale termine rilevato nel set di dati di input. Tali colonne non includono la proprietà CustomLineageID.  
  
 La tabella di ricerca deve essere una tabella di un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Access. Se l'output della trasformazione Estrazione termini viene salvato in una tabella, quest'ultima potrà essere utilizzata come tabella di riferimento, ma è possibile utilizzare anche altre tabelle. Il testo presente in file flat, cartelle di lavoro di Excel o altre origini deve essere importato in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o di Access, prima di usare la trasformazione Ricerca termini.  
  
 La trasformazione Ricerca termini utilizza una connessione OLE DB separata per connettersi alla tabella di riferimento. Per altre informazioni, vedere [Gestione connessione OLE DB](../../connection-manager/ole-db-connection-manager.md).  
  
 La trasformazione Ricerca termini funziona in una modalità con pre-memorizzazione nella cache completa. In fase di esecuzione la trasformazione Ricerca termini legge i termini dalla tabella di riferimento e li archivia nella propria memoria privata, prima di elaborare le righe di input della trasformazione.  
  
 Poiché i termini in una riga di una colonna di input possono ripetersi, l'output della trasformazione Ricerca termini include in genere un numero di righe superiore rispetto all'input.  
  
 La trasformazione include un input e un output. Non supporta output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Ricerca termini**, fare clic su uno degli argomenti seguenti:  
  
-   [Editor trasformazione Ricerca termini &#40;scheda Tabella di riferimento&#41;](../../term-lookup-transformation-editor-reference-table-tab.md)  
  
-   [Editor trasformazione Ricerca termini &#40;scheda Ricerca termini&#41;](../../term-lookup-transformation-editor-term-lookup-tab.md)  
  
-   [Editor trasformazione Ricerca termini &#40;scheda Avanzate&#41;](../../term-lookup-transformation-editor-advanced-tab.md)  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente flusso di dati](../set-the-properties-of-a-data-flow-component.md).  
  
  
