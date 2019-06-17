---
title: Avanzato Editor di Query di Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 27e7fc46-689d-43a4-9647-1c27d182bdd6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a633bd4c6a9ffe91a74858641b0b0305577922af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062794"
---
# <a name="advanced-data-mining-query-editor"></a>Editor avanzato query di data mining
  Il **Data Mining Editor avanzato Query di** è uno strumento che consente di compilare query e modelli personalizzati.  
  
 L'editor fornisce un set di modelli con collegamenti selezionabili. È sufficiente fare clic su ogni collegamento e utilizzare le finestre di dialogo per selezionare oggetti o valori e compilare istruzioni DMX complesse. È possibile passare dalla vista al modello di modifica del testo per modificare manualmente l'istruzione DMX.  
  
 Per ottenere il **Data Mining Query Editor avanzato**, fare clic su **Query** e quindi fare clic su **avanzate**.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Riquadro Query DMX**  
 In questo riquadro è possibile visualizzare l'istruzione DMX corrente.  
  
 Fare clic con il pulsante destro del mouse nel riquadro per copiare l'istruzione DMX corrente.  
  
 È possibile fare clic su una parte evidenziata dell'istruzione per visualizzare le opzioni specifiche della clausola. Ad esempio, per eliminare, aggiungere o modificare un output, fare doppio clic il  **\<Output >** collegamento.  
  
 **Modifica Query/generatore Query**  
 Usare questo pulsante per passare dall'editor di testo, in cui è possibile scrivere istruzioni DMX direttamente. e il **generatore Query**, che consente di compilare un'istruzione DMX.  
  
> [!NOTE]  
>  **Avviso:** Se si passa alle viste prima dell'esecuzione della query, viene visualizzato un messaggio che informa che si potrebbero perdere alcune modifiche. Se l'istruzione DMX è valida, in molti casi il **generatore Query** vengano convertite correttamente queste modifiche. Tuttavia, se è stata compilata un'istruzione DMX particolarmente complessa, è consigliabile salvare in modo definitivo il lavoro prima di passare alle viste.  
  
 **Modelli DMX**  
 Fare clic e selezionare in un elenco di modelli che contengono esempi DMX. I modelli forniscono quasi tutti i tipi di query di stima o del modello che potrebbero essere necessari, tra cui query con tabelle annidate, e istruzioni DMX per gestire i modelli. Anche se si ha familiarità con alcune istruzioni DMX, i modelli possono far risparmiare del tempo grazie alla sintassi appropriata.  
  
 **Scegli modello**  
 Fare clic per visualizzare un elenco di modelli di data mining disponibili nella connessione corrente.  
  
 È anche possibile visualizzare un elenco di modelli disponibili facendo clic sul nome del modello nell'istruzione DMX nel **Query DMX** riquadro. Il nome del modello è in genere evidenziato in rosso.  
  
 **Seleziona Input**  
 Fare clic per scegliere i dati da utilizzare come input per il modello di data mining. Se non è stata specificata alcuna origine dati, è anche possibile scegliere il  **\<Input >** collegamento, evidenziato in rosso nella **Query DMX** riquadro.  
  
 Selezionare **@InputRowset** nell'elenco a discesa per aprire la **Sostituisci InputRowset** dialogo casella e modificare un input esistente.  
  
 Selezionare **Aggiungi Input** per aprire il **Aggiungi Input** finestra dialogo e specificare una nuova origine dati.  
  
 È inoltre possibile modificare un input esistente facendo il **@InputRowset** collegamento, evidenziato in rosso nel riquadro Query DMX.  
  
 **Eseguire il mapping di colonne**  
 Selezionare le colonne del modello di data mining, quindi eseguirne il mapping alle colonne nell'origine dati esterna.  
  
 È anche possibile scegliere evidenziata  **\<Mapping >** collegamento nel riquadro Query DMX.  
  
 **Aggiungi output**  
 Fare clic per scegliere le colonne che devono essere restituite come output come parte di una query di stima.  
  
 È anche possibile scegliere evidenziata  **\<Aggiungi Output >** collegamento nel riquadro Query DMX.  
  
 **Colonne del modello**  
 Consente di visualizzare l'elenco delle colonne contenute nel modello di data mining selezionato. Un rombo accanto al nome della colonna indica che si tratta di una colonna stimabile.  
  
 **Colonne di input**  
 Consente di visualizzare l'elenco delle colonne dell'origine dati esterna aggiunte come input.  
  
## <a name="see-also"></a>Vedere anche  
 [Query &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](query-sql-server-data-mining-add-ins.md)  
  
  
