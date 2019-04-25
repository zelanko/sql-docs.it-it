---
title: Tabelle nidificate (Analysis Services - Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 35444ae17ac4a11bd0321e70631f45d84273e0af
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472415"
---
# <a name="nested-tables-analysis-services---data-mining"></a>Tabelle nidificate (Analysis Services - Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]i dati devono essere inseriti in un algoritmo di data mining come serie di case contenuti in una tabella del case. Non è tuttavia possibile descrivere tutti i case con una singola riga di dati. È possibile ad esempio che un case derivi da due tabelle, di cui una contiene informazioni sui clienti, l'altra gli acquisti dei clienti. Poiché a un singolo cliente nella tabella delle informazioni possono essere associati più elementi della tabella degli acquisti, potrebbe risultare difficile descrivere i dati utilizzando una sola riga. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] In *è disponibile un metodo univoco per la gestione di questi casi,* tramite tabelle annidate. Nella figura seguente viene illustrato il concetto di tabella nidificata.  
  
 ![Due tabelle combinate tramite una tabella nidificata](../../analysis-services/data-mining/media/nested-tables.gif "due tabelle combinate tramite una tabella nidificata")  
  
 Nella figura la prima tabella, che corrisponde alla tabella padre, contiene informazioni sui clienti e associa un identificatore univoco a ogni cliente. La seconda tabella, ovvero la tabella figlio, contiene gli acquisti di ciascun cliente. Tali acquisti sono correlati alla tabella padre tramite un identificatore univoco riportato nella colonna **CustomerKey** . La terza tabella della figura illustra la combinazione delle prime due tabelle.  
  
 Nella tabella del case una tabella annidata è rappresentata da una colonna speciale con tipo di dati **TABLE**. Per le righe del case questo tipo di colonna include le righe selezionate dalla tabella figlio relative alla tabella padre.  
  
 I dati di una tabella nidificata possono essere utilizzati per la stima, per l'input o per entrambi. Ad esempio, è possibile che un modello contenga due colonne di tabella nidificata: una potrebbe contenere un elenco dei prodotti acquistati dal cliente, mentre l'altra informazioni sugli hobby e gli interessi del cliente, ottenuti eventualmente da un sondaggio. In questo scenario, è possibile utilizzare gli hobby e gli interessi del cliente come input per l'analisi del comportamento di acquisto e la stima degli acquisti probabili.  
  
## <a name="joining-case-tables-and-nested-tables"></a>Unione in join di tabelle del case e tabelle nidificate  
 Per creare una tabella nidificata, è necessario che le due tabelle di origine includano una relazione definita, in modo da poter correlare gli elementi di una tabella all'altra tabella. In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]è possibile definire questa relazione nella vista origine dati.  
  
> [!NOTE]  
>  Il campo **CustomerKey** è la chiave relazionale usata per collegare la tabella del case e la tabella annidata all'interno della definizione della vista origine dati e per stabilire la relazione delle colonne all'interno della struttura di data mining. Non è tuttavia necessario in genere utilizzare questa chiave relazionale nei modelli di data mining compilati in base a tale struttura. Solitamente è preferibile omettere la colonna chiave relazionale dal modello di data mining se serve solo per unire in join le tabelle e non fornisce informazioni interessanti per l'analisi.  
  
 È possibile creare tabelle nidificate a livello di programmazione tramite DMX (Data Mining Extensions) o AMO (Analysis Management Objects) oppure tramite la Creazione guidata modello di data mining e Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="using-nested-table-columns-in-a-mining-model"></a>Utilizzo di colonne di tabelle nidificate in un modello di data mining  
 Nella tabella del case la chiave è spesso un ID cliente, un nome di prodotto o una data in una serie, ovvero dati che identificano in modo univoco una riga della tabella. tramite tabelle annidate. Nelle tabelle nidificate, tuttavia, la chiave non è in genere la chiave relazionale (o chiave esterna) ma piuttosto la colonna che rappresenta l'attributo da modellare.  
  
 Ad esempio, se la tabella del case contiene ordini e la tabella nidificata contiene gli elementi di tali ordini, non è in genere necessario modellare la relazione tra gli elementi archiviati nella tabella nidificata tra più ordini, che sono archiviati nella tabella del case. Pertanto, anche se la tabella annidata **Items** è unita in join alla tabella del case **Orders** tramite la chiave relazionale **OrderID**, non è necessario usare **OrderID** come chiave della tabella relazionale. Al contrario, è possibile selezionare la colonna **Items** come chiave della tabella annidata, poiché tale colonna contiene i dati che si desidera modellare. Nella maggior parte dei casi, è possibile ignorare in modo sicuro **OrderID** nel modello di data mining, poiché la relazione tra la tabella del case e la tabella annidata è già stata stabilita dalla definizione della vista origine dati.  
  
 Quando si sceglie una colonna da utilizzare come chiave della tabella nidificata, è necessario assicurarsi che i valori di tale colonna siano univoci per ogni case. Se ad esempio la tabella del case rappresenta i clienti e la tabella nidificata rappresenta gli elementi acquistati, è necessario assicurarsi che nessun elemento sia elencato più di una volta per ogni cliente. Se un cliente ha acquistato lo stesso elemento più di una volta, è possibile creare una vista diversa con una colonna che aggrega il conteggio degli acquisti per ogni prodotto univoco.  
  
 La decisione in merito alla gestione dei valori duplicati di una tabella nidificata dipende dal modello di data mining creato e dal problema aziendale da risolvere. In alcuni scenari può non essere importante rilevare il numero di volte in cui un cliente ha acquistato un particolare prodotto, in quanto è necessario controllare solo l'esistenza di almeno un acquisto. In altri scenari la quantità e la sequenza degli acquisti possono invece essere molto importanti.  
  
 Se l'ordine degli elementi è importante, può essere necessaria una colonna aggiuntiva che indica la sequenza. Se si usa l'algoritmo Sequence Clustering per creare un modello, è necessario scegliere una colonna *Key Sequence* aggiuntiva per rappresentare l'ordine degli elementi. Tale colonna è un tipo speciale di chiave nidificata che viene utilizzata solo nei modelli Sequence Clustering e richiede un tipo univoco di dati numerici. Ad esempio, numeri interi e date possono essere utilizzati come colonna Key Sequence, ma tutti i valori della sequenza devono essere univoci. Oltre a questa colonna, un modello di Sequence Clustering include anche una chiave di tabella nidificata che rappresenta l'attributo da modellare, ad esempio i prodotti acquistati.  
  
### <a name="using-non-key-nested-columns-from-a-nested-table"></a>Utilizzo di colonne nidificate non chiave di una tabella nidificata  
 Dopo avere definito il join tra la tabella del case e la tabella nidificata e una volta scelta una colonna che contiene attributi interessanti e univoci da utilizzare come chiave della tabella nidificata, è possibile includere altre colonne della tabella nidificata da utilizzare come input per il modello. Tutte le colonne della tabella nidificata possono essere utilizzate per l'input, per la stima e per l'input o solo per la stima.  
  
 Ad esempio, se la tabella annidata contiene le colonne **Product**, **ProductQuantity**e **ProductPrice**, è possibile scegliere **Product** come chiave della tabella annidata, ma aggiungere **ProductQuantity** alla struttura di data mining da usare come input.  
  
## <a name="filtering-nested-table-data"></a>Filtro di dati della tabella nidificata  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è possibile creare filtri sui dati da utilizzare per il training o il test del modello di data mining. Un filtro è utilizzabile per influire sulla composizione del modello o per testare il modello su un subset di case. I filtri possono anche essere applicati alle tabelle nidificate. Sono tuttavia presenti limitazioni per la sintassi che è possibile utilizzare con le tabelle nidificate.  
  
 Spesso, quando si applica un filtro a una tabella nidificata, si verifica l'esistenza o la non esistenza di un attributo. Ad esempio, è possibile applicare un filtro che limita i case utilizzati nel modello solo a quelli con un valore specificato nella tabella nidificata. Oppure è possibile limitare i case utilizzati nel modello ai clienti che non hanno acquistato un determinato elemento.  
  
 Quando si creano filtri in una tabella nidificata, è anche possibile utilizzare operatori come maggiore di o minore di. È ad esempio possibile limitare i case usati nel modello ai clienti che hanno acquistato almeno n unità del prodotto di destinazione. La possibilità di filtrare gli attributi della tabella nidificata offre una notevole flessibilità per la personalizzazione dei modelli.  
  
 Per altre informazioni su come creare e usare i filtri dei modelli, vedere [Filtri per i modelli di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Strutture di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
