---
title: Elenco di controllo della preparazione per il Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0e056c95-ba06-413e-8dc1-4d411a447c3b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c74fcbc925091a563d10bc8feef44337af48f84
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62681218"
---
# <a name="checklist-of-preparation-for-data-mining"></a>Elenco di controllo per la preparazione di data mining
  Sebbene i componenti aggiuntivi Data mining forniscano un modo piuttosto semplice e divertente per creare e provare i modelli, quando è necessario ottenere risultati ripetibili e utilizzabili, è necessario concedere il tempo appropriato per la formulazione dei requisiti aziendali di base e per il recupero e la preparazione dei dati. In questa sezione viene fornito un elenco di controllo per pianificare la ricerca e vengono descritti i problemi comuni.  
  
## <a name="checklist-of-data-preparation"></a>Elenco di controllo per la preparazione dei dati  
 **È stato identificato un output definito chiaramente.**  
 Delineare un piano per l'utilizzo dei risultati. Tipi di modelli diversi producono output diversi. Un modello Time Series genera valori per una serie in futuro, facilmente comprensibili e utilizzabili. Gli altri modelli generano set complessi che devono essere analizzati da esperti del settore per produrre il valore ottimale.  
  
-   Quale output si desidera?  
  
-   L'output può essere definito come colonna o valore singolo oppure come altro risultato utilizzabile?  
  
-   Quali sono i criteri per sapere se il modello è stato utile?  
  
-   Come verranno utilizzati e interpretati i risultati?  
  
-   È possibile eseguire il mapping dei nuovi dati di input ai risultati previsti?  
  
 **È possibile sapere il significato, i tipi di dati e la distribuzione dei dati di input.**  
 Esplorare e comprendere i dati di origine. È importante che gli utenti che esaminano il modello comprendano quale tipo di dati di input sia stato utilizzato e sappiano come interpretare i tipi di dati e la variabilità, nonché il bilanciamento e la qualità.  
  
-   Di quanti dati si dispone? Sono disponibili dati sufficienti per la modellazione?  
  
     Non deve essere una quantità enorme - più piccola e bilanciato può offrire risultati migliore.  
  
-   I dati provengono da più origini o da un'unica origine?  
  
-   I dati sono già stati elaborati e puliti? Sono disponibili più dati di input?  
  
-   È possibile sapere come lo è stato modificato prima della ricezione, - come dati potrebbero sono stati troncati, riepilogati o convertiti?  
  
-   I dati di input presentano alcuni risultati di esempio da poter utilizzare per il training?  
  
 **Dichiaro di aver compreso il livello di integrità dei dati che è disponibile e il livello che necessario.**  
 Dati errati possono influire sulla qualità del modello o impedire completamente la compilazione del modello. È necessario disporre di una buona conoscenza della distribuzione e del significato dei dati e di come sono arrivati a questo stato. È necessario comprendere se è possibile o appropriato semplificare i dati assegnando etichette, troncando i tipi di dati numerici o creando un riepilogo.  
  
-   Etichette di dati: sono chiare e corrette?  
  
-   Tipi di dati: sono appropriati e sono stati modificati?  
  
-   Sono stati ordinati, puliti o eliminati dati errati?  
  
     Si è verificato che non esistono duplicati?  
  
-   Come verranno gestiti i valori mancanti? I valori mancanti hanno un significato?  
  
-   Sono state verificate le origini per vedere se è possibile che siano stati introdotti errori nel processo di importazione?  
  
     Dov'è archiviato l'input? Per quanto tempo resta disponibile?  
  
     Esiste un dizionario dei dati? È possibile crearne uno?  
  
-   Se sono stati combinati set di dati, si è verificata la presenza di più colonne che rappresentano gli stessi dati?  
  
 **È possibile sapere dove sono archiviati i dati di origine, ovvero la provenienza e modalità di elaborazione. Il processo può essere facilmente ripetuto se necessario.**  
 Set di dati occasionale vanno bene per esperimenti, ma se si desidera spostare il modello nell'ambiente di produzione, è opportuno considerare in anticipo come applicare il processo di pulizia ai dati operativi. Inoltre, se si dispone di dati operativi, è necessario sapere come si potrebbero essere stato modificato prima della ricezione, è necessario sapere come lo era arrotondato o riepilogato.  
  
-   Si desidera poter ripetere il test?  
  
-   Quali strumenti si utilizzeranno per preparare i dati in un formato che supporta l'analisi dei dati? Possono essere automatizzati o è necessario un utente per rivederli e pulirli in Excel?  
  
-   Se si utilizzano dati provenienti da un altro sistema, sarà possibile acquisire e tenere traccia dei filtri applicati?  
  
-   Anche il framework di elaborazione dati può applicare gli algoritmi di apprendimento automatico, eseguire test e visualizzare i risultati?  
  
 **È stata decisa la granularità desiderata di stime e i dati sono stati modificati per restituire tali unità.**  
 Decidere della granularità dei risultati desiderati prima della preparazione dei dati. Ad esempio, si desidera ottenere le stime di vendita giornaliere o trimestrali? Si potrebbe provare a configurare strutture dei dati diverse per gli stessi dati, per gestire diversi livelli di riepilogo.  
  
-   Qual è l'unità di misura o l'unità di tempo corrente?  
  
     Quale unità si desidera utilizzare nei risultati?  
  
-   È possibile definire un'unità di base (ad esempio giorno / ora / minuto / chiamata istruzioni) per tutti i dati di input?  
  
     Si desidera eseguire il rollup a unità più elevate?  
  
-   Le categorie sono identificate da etichette in modo coerente? È facile aggiungere o rimuovere le categorie?  
  
 **La progettazione sperimentale è ripetibile e riproducibile.**  
 Prendere in considerazione strategie per l'analisi e la convalida dei risultati e un piano per acquisire snapshot di dati, per assicurarsi di poter far risalire gli effetti ai dati. Se viene utilizzato un valore di inizializzazione casuale, i risultati possono variare leggermente. Questa operazione può rendere difficile confrontare e convalidare i modelli.  
  
-   Se si effettuano molte modifiche personalizzate ai dati, cosa accade la volta successiva che si desidera compilare il modello?  
  
-   È stata già definita una procedura manuale o un processo approvato da utilizzare per elaborare l'input e ottenere gli output desiderati?  
  
-   Si è deciso di utilizzare un valore di inizializzazione per il modello?  
  
 **Si hanno la conoscenza del dominio per convalidare i risultati, o avere accesso a esperti del settore che possono fornire consigli.**  
 Convalidare le variabili, il modello e i risultati. Richiedere l'aiuto di esperti per valutare interazioni e risultati. Tuttavia, non consentire ai presupposti di prevalere sull'evidenza. Mostrare piena apertura verso risultati nuovi e imprevisti.  
  
-   Sono disponibili informazioni di dominio che consentono di filtrare i dati e ridurre segnalazioni non significative di input?  
  
-   Gli esperti di dominio possono aiutare a interpretare i risultati e suggerire miglioramenti?  
  
## <a name="see-also"></a>Vedere anche  
 [Scelta di dati per il data mining](choosing-data-for-data-mining.md)  
  
  
