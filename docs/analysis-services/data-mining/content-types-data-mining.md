---
title: Tipi (Data Mining) del contenuto | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0dcc5840467f039e78c0c4d4b75862bbf78a6a42
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725185"
---
# <a name="content-types-data-mining"></a>Tipi di contenuto (Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]è possibile definire sia il tipo di dati fisico per una colonna in una struttura di data mining che un tipo di contenuto logico per la colonna quando viene usata in un modello.  
  
 Il *tipo di dati* determina il modo in cui gli algoritmi elaborano i dati in tali colonne quando si creano modelli di data mining. La definizione del tipo di dati di una colonna indica all'algoritmo le informazioni sul tipo di dati delle colonne e le modalità di elaborazione dei dati. Ogni tipo di dati in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta uno o più tipi di contenuto per il data mining.  
  
 Il *tipo di contenuto* descrive il comportamento del contenuto della colonna. Se ad esempio il contenuto di una colonna si ripete in un intervallo specifico, ad esempio nell'arco dei giorni della settimana, è possibile contrassegnare il tipo di contenuto di tale colonna come ciclico.  
  
 Per il corretto funzionamento di alcuni algoritmi, sono necessari tipi di dati e tipi di contenuto specifici. L'algoritmo Microsoft Naive Bayes, ad esempio, non può utilizzare colonne continue come input, né stimare valori continui. Alcuni tipi di contenuto, ad esempio Key Sequence, sono utilizzati solo da un algoritmo specifico. Per un elenco degli algoritmi e i tipi di contenuti che supportano, vedere [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 Nell'elenco seguente vengono descritti i tipi di contenuto utilizzati nel data mining e vengono identificati i tipi di dati che supportano ogni tipo di contenuto.  
  
## <a name="discrete"></a>Discrete  
 Il tipo di contenuto*Discrete* indica che la colonna contiene un numero finito di valori senza continuità. Ad esempio, una colonna relativa al sesso è una tipica colonna attributo discreta, in quanto i dati rappresentano un numero specifico di categorie.  
  
 I valori di una colonna attributo discreta non possono implicare l'ordinamento, anche se si tratta di valori numerici. Anche se i valori utilizzati per la colonna discreta sono numerici, non è inoltre possibile calcolare valori frazionari. Gli indicativi di località telefonici sono un valido esempio di dati numerici discreti.  
  
 Il tipo di contenuto **Discrete** è supportato da tutti i tipi di dati di data mining.  
  
## <a name="continuous"></a>Continuo  
 Il tipo di contenuto*Continuous* indica che la colonna contiene valori che rappresentano dati numerici su una scala che consente valori provvisori. A differenza di una colonna discreta, che rappresenta dati numerabili finiti, una colonna continua rappresenta misure scalabili e i dati possono contenere un numero infinito di valori frazionari. Una colonna di temperature è un esempio di colonna attributo continua.  
  
 Quando una colonna contiene dati numerici continui e quando è noto il modo in cui i dati devono essere distribuiti, è possibile migliorare potenzialmente l'accuratezza dell'analisi specificando la distribuzione prevista dei valori. Poiché la distribuzione della colonna viene specificata a livello della struttura di data mining, l'impostazione si applica a tutti i modelli basati sulla struttura. Per altre informazioni, vedere [Distribuzioni delle colonne &#40;Data mining&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md).  
  
 Il **continuo** tipo di contenuto è supportato dai tipi di dati seguenti: **Data**, **doppie**, e **Long**.  
  
## <a name="discretized"></a>Discretizzato  
 Per*discretizzazione* si intende il processo di raggruppamento in bucket dei valori di un set di dati continuo in modo da limitare il numero di valori possibili. È possibile discretizzare solo dati numerici.  
  
 Di conseguenza, il tipo di contenuto *discretized* indica che la colonna contiene valori che rappresentano gruppi o bucket di valori derivati da una colonna continua. I bucket vengono considerati valori ordinati e discreti.  
  
 È possibile discretizzare i dati manualmente per ottenere i bucket desiderati oppure utilizzare i metodi di discretizzazione disponibili in SQL Server Analysis Services. Alcuni algoritmi consentono di eseguire automaticamente la discretizzazione. Per altre informazioni, vedere [Modificare la discretizzazione di una colonna in un modello di data mining](../../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md).  
  
 Il **Discretized** tipo di contenuto è supportato dai tipi di dati seguenti: **Data**, **doppie**, **Long**, e **testo**.  
  
## <a name="key"></a>Chiave  
 Il tipo di contenuto *key* indica che la colonna identifica in modo univoco una riga. In una tabella del case la colonna chiave è in genere un identificatore numerico o di testo. Impostare il tipo di contenuto su **key** per indicare che la colonna non deve essere usata per l'analisi, ma solo per la registrazione di record.  
  
 Anche le tabelle nidificate contengono chiavi, ma in questo caso l'utilizzo è leggermente diverso. Impostare il tipo di contenuto su **key** in una tabella annidata se la colonna corrisponde all'attributo che si desidera analizzare. I valori nella chiave della tabella nidificata devono essere univoci per ogni case, ma possono esistere duplicati nell'intero set di case.  
  
 Se ad esempio si analizzano i prodotti acquistati dai clienti, è possibile impostare il tipo di contenuto chiave (key) per la colonna **CustomerID** nella tabella del case e di nuovo il tipo di contenuto chiave (key) per la colonna **PurchasedProducts** nella tabella annidata.  
  
> [!NOTE]  
>  Le tabelle nidificate sono disponibili solo se si utilizzano dati di un'origine dati esterna definiti come vista origine dati di Analysis Services.  
  
 Questo tipo di contenuto è supportato dai tipi di dati seguenti: **Data**, **doppie**, **Long**, e **testo**.  
  
## <a name="key-sequence"></a>Key Sequence  
 Il tipo di contenuto *key sequence* può essere usato solo nei modelli Sequence Clustering. Quando si imposta tipo di contenuto su **key sequence**, la colonna contiene valori che rappresentano una sequenza di eventi. I valori sono ordinati, ma non è necessario che siano equidistanti.  
  
 Questo tipo di contenuto è supportato dai tipi di dati seguenti: **Doppie**, **lungo**, **testo**, e **data**.  
  
## <a name="key-time"></a>Chiave temporale  
 Il tipo di contenuto *key time* può essere usato solo nei modelli Time Series. Quando si imposta il tipo di contenuto su **key time**, i valori vengono ordinati e rappresentano una scala cronologica.  
  
 Questo tipo di contenuto è supportato dai tipi di dati seguenti: **Doppie**, **lungo**, e **data**.  
  
## <a name="table"></a>Tabella  
 Il tipo di contenuto *table* indica che la colonna contiene un'altra tabella di dati con una o più colonne e una o più righe. Questa colonna può contenere più valori per ogni determinata riga della tabella del case, tutti correlati al record del case padre. Se ad esempio la tabella del case principale contiene un elenco di clienti, è possibile disporre di molte colonne che contengono tabelle annidate, ad esempio una colonna **ProductsPurchased** , in cui la tabella annidata contiene un elenco dei prodotti acquistati da un determinato cliente nel passato e una colonna **Hobbies** in cui sono elencati gli interessi del cliente.  
  
 Il tipo di dati di questa colonna è sempre **Table**.  
  
## <a name="cyclical"></a>Cyclical  
 Il tipo di contenuto *cyclical* stabilisce che la colonna contiene valori che rappresentano un set ordinato ciclico. I giorni della settimana numerati costituiscono ad esempio un set ordinato ciclico, in quanto il giorno numero uno segue il giorno numero sette.  
  
 Le colonne cicliche vengono considerate sia ordinate che discrete in relazione al tipo di contenuto.  
  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]questo tipo di contenuto è supportato da tutti i tipi di dati del processo di data mining. Tuttavia, la maggior parte degli algoritmi trattano i valori ciclici come valori discreti e non eseguono un'elaborazione speciale.  
  
## <a name="ordered"></a>Ordered  
 Il tipo di contenuto *Ordered* indica inoltre che la colonna contiene valori che definiscono una sequenza o un ordine. In questo tipo di contenuto, tuttavia, i valori utilizzati per l'ordinamento non implicano alcuna relazione di distanza o grandezza tra i valori del set. Se ad esempio una colonna attributo ordinata contiene informazioni sui livelli di competenza elencati in ordine di priorità da uno a cinque, la distanza tra i livelli di competenza non include alcuna informazione implicita, cioè un livello di competenza pari a cinque non è necessariamente superiore a un livello di competenza pari a uno.  
  
 Le colonne attributo ordinate vengono considerate discrete in relazione al tipo di contenuto.  
  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]questo tipo di contenuto è supportato da tutti i tipi di dati del processo di data mining. Tuttavia, la maggior parte degli algoritmi trattano i valori ordinati come valori discreti e non eseguono un'elaborazione speciale.  
  
## <a name="classified"></a>Classified  
 Oltre ai tipi di contenuto precedenti che sono di uso comune con tutti i modelli, per alcuni tipi di dati è possibile utilizzare le colonne classificate per definire i tipi di contenuto. Per altre informazioni sulle colonne classificate, vedere [Colonne classificate &#40;Data mining&#41;](../../analysis-services/data-mining/classified-columns-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di contenuto &#40;DMX&#41;](../../dmx/content-types-dmx.md)   
 [Tipi di dati &#40;data mining&#41;](../../analysis-services/data-mining/data-types-data-mining.md)   
 [Tipi di dati &#40;DMX&#41;](../../dmx/data-types-dmx.md)   
 [Modificare le proprietà di una struttura di data mining](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)   
 [Colonne della struttura di data mining](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
