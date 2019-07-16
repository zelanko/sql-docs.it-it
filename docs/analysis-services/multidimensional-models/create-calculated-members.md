---
title: Creare membri calcolati | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3bfa37a34ae6c3010c36dfe7693bb6d569e6e63d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209057"
---
# <a name="create-calculated-members"></a>Creare membri calcolati
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  È possibile creare misure o membri di dimensioni personalizzati, denominati membri calcolati, combinando dati del cubo, operatori aritmetici, numeri e funzioni. È ad esempio possibile creare un membro calcolato denominato Euro in grado di convertire valori in dollari in euro moltiplicando una misura dollaro esistente per un tasso di conversione. Gli importi in euro potranno quindi essere visualizzati agli utenti finali in una riga o una colonna separata.  
  
 Le definizioni dei membri calcolati vengono archiviate, mentre i relativi valori sono presenti solo in memoria. Nell'esempio precedente, i valori in euro vengono visualizzati agli utenti finali, ma non vengono archiviati come dati del cubo.  
  
 I membri calcolati vengono creati nei cubi. Per creare un membro calcolato, nella scheda **Calcoli** di Progettazione cubi fare clic sull'icona **Nuovo membro calcolato** sulla barra degli strumenti. Verrà visualizzato un form in cui è possibile specificare le opzioni seguenti per il membro calcolato.  
  
 **Name**  
 Selezionare il nome del membro calcolato. Questo nome viene visualizzato nell'intestazione della colonna o della riga contenente i valori del membro calcolato quando gli utenti finali esplorano il cubo.  
  
 **Gerarchia padre**  
 Selezionare la gerarchia padre da includere nel membro calcolato. Le gerarchie sono categorie descrittive di una dimensione in base alle quali è possibile suddividere i dati numerici di un cubo, ovvero le misure, per l'analisi. Nei visualizzatori in formato di tabella, le gerarchie determinano le intestazioni di colonna e di riga visualizzate agli utenti finali quando esplorano i dati di un cubo. Nei visualizzatori grafici sono disponibili altri tipi di etichette descrittive, con funzione comunque identica a quella dei visualizzatori in formato di tabella. Un membro calcolato genera una nuova intestazione o etichetta nella dimensione padre selezionata.  
  
 In alternativa, è possibile includere il membro calcolato nelle misure anziché in una dimensione. Anche in questo caso viene creata una nuova intestazione di colonna o di riga, che è tuttavia associata alle misure nel visualizzatore.  
  
 **Membro padre**  
 Fare clic su **Cambia** per selezionare un membro padre in cui si desidera includere il membro calcolato. Questa opzione non è disponibile se si seleziona una gerarchia con un solo livello oppure MEASURES come dimensione padre.  
  
 Le gerarchie sono suddivise in livelli contenenti membri. Ogni membro genera un'intestazione. Durante l'esplorazione dei dati di un cubo, gli utenti finali possono eseguire il drill-down da un'intestazione selezionata alle intestazioni subordinate precedentemente nascoste. L'intestazione del membro calcolato viene aggiunta al livello immediatamente inferiore al membro padre selezionato.  
  
 **Espressione**  
 Specificare l'espressione che genera i valori del membro calcolato. Questa espressione può essere scritta in linguaggio MDX (MultiDimensional Expressions) e può contenere gli elementi seguenti:  
  
-   Espressioni di dati che rappresentano i componenti del cubo, ad esempio dimensioni, livelli, misure e così via  
  
-   Operatori aritmetici  
  
-   Numeri  
  
-   Funzioni  
  
 È possibile trascinare o copiare componenti del cubo dalla scheda **Metadati** del riquadro **Strumenti di calcolo** per aggiungerli rapidamente a un'espressione.  
  
> [!IMPORTANT]  
>  Qualsiasi membro calcolato da utilizzare nell'espressione valore di un altro membro calcolato deve essere creato prima del membro calcolato da cui viene utilizzato.  
  
 Stringa formato  
 Consente di specificare il formato dei valori di cella basati sul membro calcolato. Questa proprietà supporta gli stessi valori della proprietà **Formato di visualizzazione** delle misure. Per altre informazioni sui formati di visualizzazione, vedere [Configurare le proprietà delle misure](../../analysis-services/multidimensional-models/configure-measure-properties.md).  
  
 Visibile  
 Determina se il membro calcolato è visibile o nascosto quando vengono recuperati i metadati del cubo. Se il membro calcolato è nascosto, può comunque essere utilizzato in espressioni MDX, istruzioni e script, ma non viene visualizzato come oggetto selezionabile nelle interfacce utente client.  
  
 Gestione NON EMPTY  
 Consente di archiviare i nomi delle misure utilizzate per risolvere query NON EMPTY in MDX. Se questa proprietà è vuota, il membro calcolato dovrà essere valutato più volte per determinare se un membro è vuoto. Se questa proprietà contiene il nome di una o più misure, il membro calcolato viene considerato come vuoto se tutte le misure specificate sono vuote. Questa proprietà è un hint di ottimizzazione per Analysis Services per la restituzione solo di record non NULL. La restituzione solo dei record non NULL migliora le prestazioni delle query MDX che utilizzano l'operatore NON EMPTY o la funzione NonEmpty oppure che richiedono il calcolo dei valori delle celle. Per prestazioni ottimali nei calcolo di celle, se possibile specificare solo un singolo membro.  
  
 Espressioni colori  
 Consente di specificare le espressioni MDX che impostano in modo dinamico i colori di primo piano e di sfondo delle celle in base al valore del membro calcolato. Questa proprietà viene ignorata se non supportata dalle applicazioni client.  
  
 Espressioni caratteri  
 Consente di specificare le espressioni MDX che impostano in modo dinamico il tipo di carattere, le dimensioni di carattere e gli attributi dei caratteri per le celle in base al valore del membro calcolato. Questa proprietà viene ignorata se non supportata dalle applicazioni client.  
  
 È possibile trascinare o copiare componenti del cubo dalla scheda **Metadati** del riquadro **Strumenti di calcolo** alla casella **Espressione** nel riquadro Espressioni di calcolo. È possibile trascinare o copiare funzioni dalla scheda **Funzioni** del riquadro **Strumenti di calcolo** alla casella **Espressione** nel riquadro Espressioni di calcolo.  
  
## <a name="addressing-calculated-members"></a>Indirizzamento dei membri calcolati  
 Quando si crea un membro calcolato nella scheda **Calcoli** di **Progettazione cubi**, occorre specificare la gerarchia padre in cui tale membro viene archiviato. La gerarchia padre determina come è possibile indirizzare il membro calcolato, in base alle regole seguenti:  
  
-   Se un membro calcolato viene creato nella dimensione delle misure, sarà indirizzabile in tale dimensione.  
  
## <a name="see-also"></a>Vedere anche  
 [Calcoli nei modelli multidimensionali](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
