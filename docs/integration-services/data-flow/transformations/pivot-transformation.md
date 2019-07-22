---
title: Trasformazione Pivot | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.pivottrans.f1
helpviewer_keywords:
- Pivot transformation
- normalized data [Integration Services]
- PivotUsage property
- datasets [Integration Services], normalized data
- less normalized data set [Integration Services]
ms.assetid: 55f5db6e-6777-435f-8a06-b68c129f8437
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ca3c25c3d5b2df2427543722a4b95809a736b805
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944051"
---
# <a name="pivot-transformation"></a>Pivot - trasformazione

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La trasformazione Pivot consente di convertire un set di dati normalizzato in una versione meno normalizzata ma più compatta, trasformando i dati di input tramite Pivot in base a un valore di colonna. Un set di dati normalizzato di nome **Orders** che elenca nomi di clienti, prodotti e quantità vendute, ad esempio, include in genere più righe per ogni cliente che ha acquistato più prodotti, indicando su ogni riga i dettagli dell'ordine di un prodotto specifico. Trasformando il set di dati tramite Pivot in base alla colonna dei prodotti, la trasformazione Pivot può restituire in output un set di dati con una singola riga per cliente, nella quale sono elencati tutti gli acquisti effettuati dal cliente, utilizzando i nomi dei prodotti come nomi delle colonne e visualizzando le quantità come valori nelle colonne dei prodotti. Poiché non tutti i clienti acquistano tutti i prodotti, molte colonne possono contenere valori Null.  
  
 Quando si trasforma un set di dati tramite Pivot, le colonne di input svolgono ruoli diversi nel processo. Una colonna può partecipare nei modi seguenti:  
  
-   La colonna viene passata all'output invariata. Poiché più righe di input possono convergere in una sola riga di output, la trasformazione copia solo il primo valore di input per la colonna.  
  
-   La colonna viene utilizzata come chiave, o parte di una chiave, che identifica un set di record.  
  
-   La colonna definisce il pivot. I valori nella colonna vengono associati alle colonne del set di dati trasformato tramite Pivot.  
  
-   La colonna contiene valori che vengono inseriti nelle colonne create dalla trasformazione Pivot.  
  
 Questa trasformazione include un input, un output regolare e un output degli errori.  
  
## <a name="sort-and-duplicate-rows"></a>Ordinare e duplicare le righe  
 Per trasformare efficientemente i dati tramite Pivot, ovvero creare il minor numero di record possibile nel set di dati di output, i dati di input devono essere ordinati in base alla colonna pivot. Se i dati non sono ordinati, la trasformazione Pivot potrà generare più record per ogni valore nella chiave del set, che è la colonna che definisce l'appartenenza al set. Se un set di dati viene trasformato tramite Pivot in base a una colonna **Name** , ad esempio, ma i nomi non sono ordinati, nel set di dati di output potranno essere incluse più righe per ogni cliente, perché viene eseguita un'operazione pivot ogni volta che cambia il valore in **Name** .  
  
 I dati di input potrebbero contenere righe duplicate, provocando l'errore della trasformazione Pivot. Per righe duplicate si intendono righe che contengono gli stessi valori nelle colonne chiave del set e nelle colonne pivot. Per evitare l'errore è possibile configurare la trasformazione in modo che le righe con esito negativo vengano reindirizzate a un output degli errori, oppure preaggregare i valori per assicurarsi che non siano presenti righe duplicate.  
  
##  <a name="options"></a> Opzioni della finestra di dialogo Pivot  
 L'operazione pivot può essere configurata impostando le opzioni nella finestra di dialogo **Pivot** . Per aprire la finestra di dialogo **Pivot** , aggiungere la trasformazione Pivot al pacchetto in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]e quindi fare clic con il pulsante destro del mouse sul componente e scegliere **Modifica**.  
  
 L'elenco seguente descrive le opzioni nella finestra di dialogo **Pivot** .  
  
 **Chiave pivot**  
 Viene specificata la colonna da utilizzare per i valori nella riga superiore (riga di intestazione) della tabella.  
  
 **Chiave set**  
 Viene specificata la colonna da utilizzare per i valori nella colonna sinistra della tabella. È necessario ordinare la data di input in questa colonna.  
  
 **Valore pivot**  
 Viene specificata la colonna da utilizzare per i valori della tabella diversi rispetto ai valori della riga di intestazione e della colonna sinistra.  
  
 **Ignora i valori delle chiavi pivot senza corrispondenza e segnalali dopo l'esecuzione del flusso di dati**  
 Selezionare questa opzione per configurare la trasformazione Pivot per ignorare le righe contenenti valori non riconosciuti nella colonna **Chiave pivot** e restituire tutti i valori di chiave pivot in un messaggio di log, quando viene eseguito il pacchetto.  
  
 È anche possibile configurare la trasformazione per restituire i valori impostando la proprietà personalizzata **PassThroughUnmatchedPivotKeys** su **True**.  
  
 **Generare colonne di output pivot dai valori**  
 Immettere i valori di chiave pivot in questa casella per consentire alla trasformazione Pivot di creare colonne di output per ogni valore. È possibile immettere i valori prima dell'esecuzione del pacchetto oppure effettuare le operazioni seguenti.  
  
1.  Selezionare l'opzione **Ignora i valori delle chiavi pivot senza corrispondenza e segnalali dopo l'esecuzione del flusso di dati** , quindi fare clic su **OK** nella finestra di dialogo **Pivot** per salvare le modifiche nella trasformazione Pivot.  
  
2.  Eseguire il pacchetto.  
  
3.  Quando l'esecuzione del pacchetto viene completata correttamente, fare clic sulla scheda **Stato** e cercare il messaggio di log informativo della trasformazione Pivot contenente i valori di chiave pivot.  
  
4.  Fare clic con il pulsante destro del mouse sul messaggio e scegliere **Copia testo messaggio**.  
  
5.  Fare clic su **Arresta debug** nel menu **Debug** per passare alla modalità progettazione.  
  
6.  Fare clic con il pulsante destro del mouse sulla trasformazione Pivot e quindi scegliere **Modifica**.  
  
7.  Deselezionare l'opzione **Ignora i valori delle chiavi pivot senza corrispondenza e segnalali dopo l'esecuzione del flusso di dati** , quindi incollare i valori di chiave pivot nella casella **Generare colonne di output pivot dai valori** usando il formato seguente.  
  
     [valore1],[valore2],[valore3]  
  
 **Genera colonne**  
 Fare clic per creare una colonna di output per ogni valore di chiave pivot elencato nella casella **Generare colonne di output pivot dai valori** .  
  
 Le colonne di output vengono visualizzate nella casella **Colonne di output trasformate tramite pivot esistenti** .  
  
 **Colonne di output trasformate tramite pivot esistenti**  
 Vengono elencate le colonne di output per i valori di chiave pivot  
  
 La tabella seguente mostra un set di dati prima della trasformazione dei dati tramite Pivot in base alla colonna **Year** .  
  
|Year|Nome prodotto|Total|  
|----------|------------------|-----------|  
|2004|HL Mountain Tire|1504884.15|  
|2003|Road Tire Tube|35920.50|  
|2004|Water Bottle - 30 oz.|2805.00|  
|2002|Touring Tire|62364.225|  
  
 La tabella seguente mostra un set di dati dopo la trasformazione dei dati tramite Pivot in base alla colonna **Year** .  
  
||2002|2003|2004|  
|-|----------|----------|----------|  
|HL Mountain Tire|141164.10|446297.775|1504884.15|  
|Road Tire Tube|3592.05|35920.50|89801.25|  
|Water Bottle - 30 oz.|*NULL*|*NULL*|2805.00|  
|Touring Tire|62364.225|375051.60|1041810.00|  
  
 Per trasformare i dati tramite Pivot in base alla colonna **Year** , come mostrato in precedenza, vengono impostate le opzioni seguenti nella finestra di dialogo **Pivot** .  
  
-   Selezione di Year nella casella di riepilogo **Chiave pivot** .  
  
-   Selezione di Product Name nella casella di riepilogo **Chiave set** .  
  
-   Selezione di Total nella casella di riepilogo **Valore pivot** .  
  
-   Immissione dei valori seguenti nella casella **Generare colonne di output pivot dai valori** .  
  
     [2002],[2003],[2004]  
  
## <a name="configuration-of-the-pivot-transformation"></a>Configurazione della trasformazione Pivot  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** , fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Per informazioni su come impostare le proprietà del componente, vedere [Impostare le proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione UnPivot](../../../integration-services/data-flow/transformations/unpivot-transformation.md)   
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
