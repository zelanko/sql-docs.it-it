---
title: Editor avanzato query di data mining | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 27e7fc46-689d-43a4-9647-1c27d182bdd6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 90a64369c76e254e509f5f57b1da29ededeed08f
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528197"
---
# <a name="advanced-data-mining-query-editor"></a>Editor avanzato query di data mining
  Il **Editor avanzato di query di data mining** è uno strumento che consente di compilare modelli e query personalizzati.  
  
 L'editor fornisce un set di modelli con collegamenti selezionabili. È sufficiente fare clic su ogni collegamento e utilizzare le finestre di dialogo per selezionare oggetti o valori e compilare istruzioni DMX complesse. È possibile passare dalla vista al modello di modifica del testo per modificare manualmente l'istruzione DMX.  
  
 Per ottenere la **Editor avanzato di query di data mining**, fare clic su **query** e quindi su **Avanzate**.  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
 **Riquadro Query DMX**  
 In questo riquadro è possibile visualizzare l'istruzione DMX corrente.  
  
 Fare clic con il pulsante destro del mouse nel riquadro per copiare l'istruzione DMX corrente.  
  
 È possibile fare clic su una parte evidenziata dell'istruzione per visualizzare le opzioni specifiche della clausola. Per eliminare, aggiungere o modificare un output, ad esempio, fare clic con il pulsante destro del mouse sul **\<Output>** collegamento.  
  
 **Modifica query/Generatore query**  
 Utilizzare questo pulsante per cambiare l'Editor tra un editor di testo, in cui è possibile scrivere direttamente istruzioni DMX; e la **Generatore di query**, che consente di compilare un'istruzione DMX.  
  
> [!NOTE]  
>  **Avviso:** Se si cambiano le visualizzazioni prima dell'esecuzione della query, viene visualizzato un messaggio che informa che è possibile che si perdano alcune modifiche. Se l'istruzione DMX è valida, in molti casi l' **Generatore di query** potrebbe convertire correttamente le modifiche. Tuttavia, se è stata compilata un'istruzione DMX particolarmente complessa, è consigliabile salvare in modo definitivo il lavoro prima di passare alle viste.  
  
 **Modelli DMX**  
 Fare clic e selezionare in un elenco di modelli che contengono esempi DMX. I modelli forniscono quasi tutti i tipi di query di stima o del modello che potrebbero essere necessari, tra cui query con tabelle annidate, e istruzioni DMX per gestire i modelli. Anche se si ha familiarità con alcune istruzioni DMX, i modelli possono far risparmiare del tempo grazie alla sintassi appropriata.  
  
 **Scegli modello**  
 Fare clic per visualizzare un elenco di modelli di data mining disponibili nella connessione corrente.  
  
 È inoltre possibile visualizzare un elenco dei modelli disponibili facendo clic sul nome del modello nell'istruzione DMX nel riquadro **query DMX** . Il nome del modello è in genere evidenziato in rosso.  
  
 **Selezionare l'input**  
 Fare clic per scegliere i dati da utilizzare come input per il modello di data mining. Se non è stata specificata alcuna origine dati, è anche possibile fare clic sul **\<Input>** collegamento, evidenziato in rosso nel riquadro **query DMX** .  
  
 Selezionare ** \@ InputRowset** nell'elenco a discesa per aprire la finestra di dialogo **Sostituisci InputRowset** e modificare un input esistente.  
  
 Selezionare **Aggiungi input** per aprire la finestra di dialogo **Aggiungi input** e specificare una nuova origine dati.  
  
 È anche possibile modificare un input esistente facendo clic sul collegamento ** \@ InputRowset** , evidenziato in rosso nel riquadro query DMX.  
  
 **Mappa colonne**  
 Selezionare le colonne del modello di data mining, quindi eseguirne il mapping alle colonne nell'origine dati esterna.  
  
 È inoltre possibile fare clic sul **\<Mapping>** collegamento evidenziato nel riquadro query DMX.  
  
 **Aggiungi output**  
 Fare clic per scegliere le colonne che devono essere restituite come output come parte di una query di stima.  
  
 È inoltre possibile fare clic sul **\<Add Output>** collegamento evidenziato nel riquadro query DMX.  
  
 **Colonne modello**  
 Consente di visualizzare l'elenco delle colonne contenute nel modello di data mining selezionato. Un rombo accanto al nome della colonna indica che si tratta di una colonna stimabile.  
  
 **Colonne di input**  
 Consente di visualizzare l'elenco delle colonne dell'origine dati esterna aggiunte come input.  
  
## <a name="see-also"></a>Vedere anche  
 [&#40;di query SQL Server componenti aggiuntivi Data mining&#41;](query-sql-server-data-mining-add-ins.md)  
  
  
