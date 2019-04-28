---
title: Aggiunta di un tipo di dati della vista origine per dati di Call Center (esercitazione intermedia di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a448e7e4-dbd1-4d31-90bc-4d4a1c23b352
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5da7978db04b0fdf6e1d4f7740857fc5c0cf90ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823301"
---
# <a name="adding-a-data-source-view-for-call-center-data-intermediate-data-mining-tutorial"></a>Aggiunta di una vista origine dati per i dati del call center (Esercitazione intermedia sul data mining)
  In questa attività verrà aggiunta una vista origine dati da utilizzare per accedere ai dati del call center. Gli stessi dati verranno utilizzati per compilare sia il modello di rete neurale iniziale per l'esplorazione, sia il modello di regressione logistica che verrà utilizzato per preparare i consigli.  
  
 Si utilizzerà inoltre la finestra di progettazione Vista origine dati per aggiungere una colonna per il giorno feriale. Questa operazione è necessaria poiché, anche se i dati di origine tengono traccia dei dati del call center in base alle date, l'esperienza insegna che sono presenti modelli ricorrenti sia in termini di volume di chiamate che di qualità del servizio, a seconda se il giorno è un fine settimana o un giorno feriale.  
  
## <a name="procedures"></a>Procedure  
  
#### <a name="to-add-a-data-source-view"></a>Per aggiungere una vista origine dati  
  
1.  Nelle **Esplora soluzioni**, fare doppio clic su **viste origine dati**e selezionare **nuova vista origine dati**.  
  
     Verrà avviata Creazione guidata vista origine dati.  
  
2.  Nella pagina iniziale di **Creazione guidata vista origine dati** fare clic su **Avanti**.  
  
3.  Nel **Vybrat Zdroj** nella pagina **origini dati relazionali**, selezionare il [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] zdroj dat. Se non hai questa origine dati, vedere [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md). Scegliere **Avanti**.  
  
4.  Nel **selezione tabelle e viste** pagina, selezionare la tabella seguente e quindi fare clic sulla freccia a destra per aggiungerla alla vista origine dati:  
  
    -   **FactCallCenter (dbo)**  
  
    -   **DimDate**  
  
5.  Scegliere **Avanti**.  
  
6.  Nel **Completamento procedura guidata** pagina, per impostazione predefinita la vista origine dati è denominata [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]. Modificare il nome in **CallCenter**, quindi fare clic su **fine**.  
  
     Verrà aperto Progettazione vista origine dati per visualizzare il **CallCenter** vista origine dati.  
  
7.  All'interno del riquadro Vista origine dati e scegliere **Aggiungi/Rimuovi tabelle**. Selezionare la tabella **DimDate** e fare clic su **OK**.  
  
     Una relazione deve essere aggiunto automaticamente tra il `DateKey` colonne in ogni tabella. Si utilizzerà questa relazione per ottenere la colonna **EnglishDayNameOfWeek**, dalle **DimDate** di tabella e usarlo nel modello.  
  
8.  Nella finestra di progettazione vista origine dati, fare doppio clic nella tabella **FactCallCenter**e selezionare **nuovo calcolo denominato**.  
  
     Nel **Crea calcolo denominato** finestra di dialogo, digitare i valori seguenti:  
  
    |||  
    |-|-|  
    |**Nome colonna**|DayOfWeek|  
    |**Descrizione**|Ottenere il giorno di settimana dalla tabella DimDate|  
    |**Espressione**|`(SELECT EnglishDayNameOfWeek AS DayOfWeek FROM DimDate where FactCallCenter.DateKey = DimDate.DateKey)`|  
  
     Per verificare che l'espressione crei i dati è necessario, fare doppio clic nella tabella **FactCallCenter**, quindi selezionare **Esplora dati**.  
  
9. Rivedere i dati disponibili, in modo da comprendere come vengono utilizzati nel data mining:  
  
|Nome colonna|Contiene|  
|-----------------|--------------|  
|FactCallCenterID|Una chiave arbitraria creata durante l'importazione dei dati nel data warehouse.<br /><br /> Questa colonna identifica record univoci e deve essere utilizzata come chiave del case per il modello di data mining.|  
|DateKey|La data dell'operazione del call center, espressa come un Integer. Le chiavi della data di tipo Integer vengono spesso utilizzate nei data warehouse, ma è consigliabile ottenere la data nel formato di data/ora se si prevede di eseguire il raggruppamento in base ai valori di data.<br /><br /> Le date non sono univoche perché il fornitore presenta un report distinto per ogni turno di ogni giorno lavorativo.|  
|WageType|Viene indicato se il giorno è un giorno feriale, festivo o un fine settimana.<br /><br /> È possibile che vi sia una differenza nella qualità del servizio clienti nei fine settimana e giorni della settimana, quindi si utilizzerà questa colonna come input.|  
|Turno|Indica il turno per il quale vengono registrate le chiamate. Questo call center divide il giorno lavorativo in quattro turni: AM, PM1, PM2 e Midnight.<br /><br /> È possibile che il turno influisca sulla qualità del servizio clienti, quindi si utilizzerà questa colonna come input.|  
|LevelOneOperators|Indica il numero di operatori di livello 1 in servizio.<br /><br /> I dipendenti del call center iniziano a Livello 1, pertanto questi dipendenti sono meno esperti.|  
|LevelTwoOperators|Indica il numero di operatori di livello 2 in servizio.<br /><br /> Per qualificarsi come operatore di livello 2, un dipendente deve registrare un determinato numero di ore di servizio.|  
|TotalOperators|Numero complessivo di operatori presenti durante il turno.|  
|Calls|Numero di chiamate ricevute durante il turno.|  
|AutomaticResponses|Numero di chiamate gestite completamente dall'elaborazione automatica delle chiamate (Interactive Voice Response o IVR).|  
|Orders|Numero di ordini risultanti dalle chiamate.|  
|IssuesRaised|Numero di problemi generati dalle chiamate che richiedono una soluzione.|  
|AverageTimePerIssue|Tempo medio richiesto per rispondere a una chiamata in entrata.|  
|ServiceGrade|Una metrica che indica la qualità generale del servizio, misurata come il *frequenza di abbandono* per l'intero turno. Più elevata è la frequenza di abbandono, più è probabile che i clienti siano scontenti e che gli ordini potenziali non vengano conclusi.|  
  
 Si noti che i dati includono quattro colonne diverse basate su una singola colonna di data: `WageType`, **DayOfWeek**, `Shift`, e `DateKey`. Solitamente nel data mining non è consigliabile utilizzare più colonne derivate dagli stessi dati, in quanto i valori sono correlati troppo strettamente tra di essi e possono nascondere altri modelli.  
  
 Tuttavia, non utilizzeremo `DateKey` nel modello perché contiene troppi valori univoci. Senza alcuna relazione diretta tra `Shift` e **DayOfWeek**, e `WageType` e **DayOfWeek** sono correlati solo in parte. Se la collinearità è importante, è possibile creare la struttura utilizzando tutte le colonne disponibili, quindi ignorare le colonne diverse in ogni modello e testare l'effetto.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di una struttura di rete neurale e il modello &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
