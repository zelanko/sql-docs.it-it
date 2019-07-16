---
title: Le misure e gruppi di misure | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 04eb5a41bec6e9abb62cfde516f2dad2ff820521
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165744"
---
# <a name="measures-and-measure-groups"></a>Misure e gruppi di misure
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un cubo include *misure* in *gruppi di misure*, logica di business e una raccolta di dimensioni che forniscono il contesto per la valutazione dei dati numerici specificati da una misura. Misure e gruppi di misure sono componenti essenziali di un cubo. Un cubo non può esistere senza almeno una misura e un gruppo di misure.  
  
 Questo argomento descrive le [misure](#bkmk_measure) e i [gruppi di misure](#bkmk_mg). Include anche la tabella seguente, con collegamenti alle procedure per la creazione e configurazione di misure e di gruppi di misure.  
  
|**Collegamento**|**Descrizione**|  
|--------------|---------------------|  
|[Creare misure e gruppi di misure nei modelli multidimensionali](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|Scegliere uno dei diversi approcci per la creazione di misure e gruppi di misure.|  
|[Configurare le proprietà delle misure](../../analysis-services/multidimensional-models/configure-measure-properties.md)|Se è stata usata la Creazione guidata cubo per avviare il cubo, è necessario modificare il metodo di aggregazione, applicare un formato dati, impostare la visibilità della misura in applicazioni client o eventualmente aggiungere un'espressione di misura per modificare i dati prima che i valori vengano aggregati.|  
|[Configurare le proprietà dei gruppi di misure](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)|In un modello multidimensionale, un gruppo di misure equivale a una tabella dei fatti nel data warehouse di origine. Le proprietà in un gruppo di misure consentono di specificare i comportamenti di memorizzazione nella cache, l'archiviazione e l'elaborazione delle istruzioni che operano collettivamente a livello del gruppo di misure. La configurazione della partizione dipende in parte dalle proprietà impostate per gli oggetti del gruppo di misure.|  
|[Utilizzare le funzioni di aggregazione](../../analysis-services/multidimensional-models/use-aggregate-functions.md)|Informazioni sui metodi di aggregazione che possono essere assegnati a una misura.|  
|[Definire una funzione semiadditiva](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)|Le funzioni semiadditive fanno riferimento alle aggregazioni valide solo per alcune dimensioni. Un esempio comune è un saldo del conto bancario. L'utente potrebbe voler aggregare i saldi in base al cliente e alla regione, ma non al tempo. Ad esempio, l'utente potrebbe non voler aggiungere i saldi dallo stesso conto per più giorni consecutivi. Per definire le funzioni semiadditive, usare la procedura guidata Aggiungi funzionalità di Business Intelligence.|  
|[Gruppi di misure collegati](../../analysis-services/multidimensional-models/linked-measure-groups.md)|Ridefinire un gruppo di misure esistente in altri cubi dello stesso database o in diversi database di Analysis Services.|  
  
##  <a name="bkmk_measure"></a> Measures  
 Una misura rappresenta una colonna contenente dati quantificabili, spesso di tipo numerico, che è possibile aggregare. Le misure rappresentano alcuni aspetti delle attività aziendali espressi in termini monetari (ad esempio ricavi, margini o costi), sotto forma di conteggi (livelli di inventario, numero di dipendenti, clienti o ordini) o come calcoli più complessi che incorporano la logica di business.  
  
 Ogni cubo deve avere almeno una misura, ma in genere il numero di misure associate è elevato e può raggiungere le centinaia. A livello di struttura, una misura viene spesso mappata a una colonna di origine in una tabella dei fatti e tale colonna fornisce i valori usati per caricare la misura. In alternativa, è possibile definire una misura usando MDX.  
  
 Le misure sono sensibili al contesto perché operano sui dati numerici di un contesto determinati dai membri della dimensione inclusi nella query. Ad esempio, una misura che calcola **Vendite rivenditore** sarà supportata da un operatore **Sum** e aggiungerà gli importi delle vendite per ogni membro di dimensione incluso nella query. Se la query specifica singoli prodotti, esegue il rollup in una categoria o è suddivisa in base al tempo o all'area geografica, la misura deve produrre un'operazione valida per le dimensioni incluse nella query.  
  
 In questo esempio il valore di **Vendite rivenditore** viene aggregato in diversi livelli della gerarchia **Territorio vendita** .  
  
 ![Tabella pivot con misure e dimensioni indicate](../../analysis-services/multidimensional-models/media/ssas-keyconcepts-pivot1-measures-dimensions.png "tabella pivot con misure e dimensioni indicate")  
  
 Le misure producono risultati validi quando la tabella dei fatti che contiene i dati numerici di origine comprende anche i puntatori alle tabelle delle dimensioni usate nella query. Usando l'esempio di Vendite rivenditore, se in ogni riga dove viene archiviato un importo di vendita viene archiviato anche un puntatore a una tabella prodotto, a una tabella data o a una tabella area di vendita, le query che includono i membri di queste dimensioni verranno risolte correttamente.  
  
 Cosa accade se la misura non è correlata alle dimensioni usate nella query? Di norma, Analysis Services visualizzerà la misura predefinita e il valore sarà lo stesso per tutti i membri. In questo esempio, **Vendite Internet**, che misura le vendite dirette effettuate dai clienti usando il catalogo online, non ha alcuna relazione con l'organizzazione addetta alle vendite.  
  
 ![I valori di tabella pivot che mostra ripetute misure](../../analysis-services/multidimensional-models/media/ssas-unrelatedmeasure.PNG "valori di tabella pivot che mostra ripetute misure")  
  
 Per ridurre al minimo la probabilità che questi comportamenti si verifichino in un'applicazione client, è possibile creare più cubi o prospettive nello stesso database e assicurarsi che ogni cubo o prospettiva contenga solo gli oggetti correlati. Le relazioni da controllare sono quelle tra il gruppo di misure (mappato alla tabella dei fatti) e le dimensioni.  
  
##  <a name="bkmk_mg"></a> Measure Groups  
 In un cubo le misure vengono raggruppate in gruppi di misure in base alle tabelle dei fatti sottostanti. I gruppi di misure consentono di associare dimensioni a misure. Vengono inoltre utilizzati per misure con la modalità di aggregazione Distinct Count. Il posizionamento di ogni misura Distinct Count nel relativo gruppo di misure consente di ottimizzare l'elaborazione delle aggregazioni.  
  
 Un oggetto <xref:Microsoft.AnalysisServices.MeasureGroup> semplice è composto da informazioni di base come nome del gruppo, modalità di archiviazione e modalità di elaborazione. Contiene inoltre le relative parti costituenti: misure, dimensioni e partizioni che formano la composizione del gruppo di misure.  
  
## <a name="see-also"></a>Vedere anche  
 [Cubi nei modelli multidimensionali](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)   
 [Creare misure e gruppi di misure nei modelli multidimensionali](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)  
  
  
