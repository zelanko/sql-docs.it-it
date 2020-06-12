---
title: Riquadro di progettazione (visualizzazione Stima modello di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.prediction.design.f1
ms.assetid: 17f24c8d-43cd-4f4d-83b3-a41ee8fbe8e8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 32ac73a2d6fde38d15d1f45a8439293695749ea4
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528697"
---
# <a name="design-pane-mining-model-prediction-view"></a>Riquadro Progettazione (visualizzazione Stima modello di data mining)
  Il riquadro **Progettazione** contiene il generatore delle query di stima che consente di compilare le stime di data mining. È possibile progettare query di stima che utilizzano tabelle di dati di input da una vista origine dati per generare stime bulk oppure creare query di stima singleton per fornire valori singoli.  
  
 Per eseguire la query e visualizzare i risultati, passare alla visualizzazione dei risultati della query.  
  
 Nella visualizzazione **Query** viene visualizzata la query DMX (Data Mining Extensions) creata dal generatore delle query di stima. Se si ha dimestichezza con DMX, è possibile personalizzare questa query.  
  
> [!NOTE]  
>  Qualsiasi modifica manuale eventualmente apportata alla query andrà perduta quando si torna alla visualizzazione della struttura. Per salvare la query DMX, è possibile copiarla negli Appunti di Windows e incollarla quindi in un file di testo.  
  
 **Per altre informazioni, vedere** [Query di data mining](data-mining/data-mining-queries.md)  
  
## <a name="options"></a>Opzioni  
 **Passa alla visualizzazione dei risultati della query**  
 Fare clic su questo pulsante per spostarsi tra i riquadri **Progettazione**, **Query**e **Risultato** . Se si passa al riquadro **Risultato** , verrà eseguita la query.  
  
 **Salva risultati query**  
 Consente di aprire la finestra di dialogo **Salva risultati query di data mining** .  
  
 **Query singleton**  
 Consente di attivare la creazione di un query singleton nella quale è possibile fornire direttamente i valori per la query anziché specificare una tabella come origine dei dati noti. La tabella **Seleziona tabelle di input** viene sostituita dalla tabella **Input query singleton** .  
  
 **Aggiorna risultati query**  
 Consente di rielaborare la query di stima. Questa opzione è attivata solo nel riquadro **Risultato** .  
  
 **Modello di data mining**  
 Consente di visualizzare il modello di data mining selezionato sul quale si desidera basare le stime.  
  
 **Seleziona modello**  
 Consente di aprire la finestra di dialogo **Seleziona modello di data mining** .  
  
 **Seleziona tabella/e di input**  
 Consente di visualizzare le tabelle di input selezionate contenenti dati noti su cui basare le stime.  
  
 **Elimina tabella**  
 Consente di eliminare la tabella selezionata. Questo pulsante è disabilitato se non è stata selezionata una tabella o non esiste.  
  
 **Seleziona tabella del case**  
 Consente di aprire la finestra di dialogo **Seleziona tabella** . Questo pulsante è disponibile solo se non è stata selezionata una tabella.  
  
 **Seleziona tabella nidificata**  
 Consente di aprire la finestra di dialogo **Seleziona tabella** . Questo pulsante viene visualizzato solo se è stata selezionata una tabella del case. Se nella struttura di data mining associata non è inclusa una tabella nidificata, il pulsante è disabilitato.  
  
 **Modifica join**  
 Consente di aprire la finestra di dialogo **Specifica join nidificato** . Questo pulsante è attivo solo se si seleziona una tabella nidificata.  
  
 **Input query singleton**  
 Questa opzione viene attivata quando si sceglie il pulsante **Query singleton** e presenta le colonne seguenti:  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**Colonna modello di data mining**|Elenca le colonne del modello di data mining contenute nel modello di data mining selezionato nella tabella **Modello di data mining** .|  
|**Valore**|Consente di selezionare un valore nell'elenco che contiene ogni possibile stato della colonna del modello di data mining selezionata.<br /><br /> Se la colonna è la colonna di una tabella nidificata, fare clic sulla cella del valore per aprire la finestra di dialogo **Input tabella nidificata** .|  
  
 **origine**  
 Consente di selezionare l'origine contenente il campo che verrà utilizzato per la colonna. È possibile usare il modello di data mining selezionato nella tabella **Modello di data mining** , la tabella o le tabelle di input selezionate nella tabella **Seleziona tabella/e di input** , una funzione di stima o un'espressione personalizzata.  
  
 È possibile trascinare le colonne dalle tabelle contenenti il modello di data mining e dalle tabelle di input sulla cella.  
  
 **Campo**  
 Consente di selezionare una colonna nell'elenco di colonne derivato dalla tabella di origine. Se è stata selezionata l'opzione **Funzione di stima** in **Origine**, l'elenco conterrà la funzione di stima disponibile per il modello di data mining specificato.  
  
 **Gruppo**  
 Usare questa opzione con la colonna **And/Or** per raggruppare le espressioni. Ad esempio, `(expr1 Or expr2) And expr3`  
  
 **E/o**  
 Utilizzare questa opzione per creare una query logica. Ad esempio, `(expr1 Or expr2) And expr3`  
  
 **Criteri/Argomento**  
 Consente di specificare una condizione o un'espressione utente da applicare a una colonna. È possibile trascinare le colonne dalle tabelle contenenti il modello di data mining e dalle tabelle di input sulla cella.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](/sql/dmx/data-mining-extensions-dmx-statements)   
 [Interfacce di query di data mining](data-mining/data-mining-query-tools.md)   
 [Generatore delle query di stima &#40;Data Mining&#41;](prediction-query-builder-data-mining.md)  
  
  
