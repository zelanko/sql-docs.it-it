---
title: Il linguaggio DAX nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e62c50026d391db37beca5844da24eae43f12014
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072448"
---
# <a name="dax-in-tabular-models"></a>DAX nei modelli tabulari 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Data Analysis Expressions (DAX) è un linguaggio delle formule utilizzato per creare calcoli personalizzati in Analysis Services, Power BI Desktop e Power Pivot in Excel. Le formule DAX includono funzioni, operatori e valori che consentono di eseguire calcoli avanzati sui dati in tabelle e colonne.  
  
 Mentre DAX viene utilizzato in Analysis Services, Power BI Desktop e Power Pivot in Excel, in questo argomento si applica più ai progetti di modello tabulare di Analysis Services creati in SQL Server Data Tools (SSDT).  
  
##  <a name="bkmk_DAX"></a> Formule DAX in colonne calcolate, misure e filtri di riga  
 Per modelli tabulari creati in SSDT, vengono utilizzate le formule DAX in colonne calcolate, misure e filtri di riga.  
  
### <a name="calculated-columns"></a>Colonne calcolate  
 Una colonna calcolata è una colonna che si aggiunge a una tabella esistente (in Progettazione modelli) e quindi crea una formula DAX che definisce i valori della colonna. 
  
> [!NOTE]  
>  Le colonne calcolate non sono supportate per i modelli in cui i dati vengono recuperati da un'origine dati relazionale tramite la modalità DirectQuery.  
  
 Quando una colonna calcolata contiene una formula DAX valida, i valori vengono calcolati per ogni riga non appena si immette la formula. I valori vengono quindi archiviati nel database. Ad esempio, quando in una tabella Date si immette la formula `=[Calendar Year] & " Q" & [Calendar Quarter]` nella barra della formula, viene calcolato un valore per ogni riga della tabella utilizzando i valori della colonna Calendar Year (nella stessa tabella Date), aggiungendo uno spazio e la lettera maiuscola Q, quindi i valori della colonna Calendar Quarter (nella stessa tabella Date). Per ogni riga nella colonna calcolata viene calcolato immediatamente il risultato che sarà visualizzato, ad esempio, come **2010 Q1**. I valori della colonna vengono ricalcolati solo se vengono elaborati nuovamente i dati.  
  
 Per altre informazioni, vedere [Colonne calcolate](../../analysis-services/tabular-models/ssas-calculated-columns.md).  
  
### <a name="measures"></a>Misure  
 Le misure sono formule dinamiche in cui i risultati vengono modificati a seconda del contesto. Le misure vengono utilizzate in formati di report che supportano la combinazione e il filtro dei dati del modello utilizzando più attributi, ad esempio un report di Power BI o una tabella pivot di Excel o un grafico pivot. Le misure sono definite dall'autore del modello tramite la griglia delle misure (e barra della formula) nella finestra di progettazione del modello in SSDT.  
  
 Nella formula di una misura possono essere utilizzate funzioni di aggregazione standard create automaticamente con la funzionalità Somma automatica, ad esempio COUNT o SUM. In alternativa, è possibile definire formule personalizzate tramite DAX. Quando si definisce una formula per una misura nella barra della formula, tramite una descrizione comando viene visualizzata un'anteprima dei possibili risultati per il totale nel contesto corrente. Generalmente i risultati non vengono restituiti immediatamente in nessuna posizione. Altri dettagli relativi alla misura vengono visualizzati anche nel riquadro **Proprietà** .  
  
 Il motivo per cui non è possibile visualizzare i risultati (filtrati) del calcolo immediatamente è dovuto al fatto che il risultato di una misura non può essere determinato senza contesto. La valutazione di una misura richiede la presenza di un'applicazione client di creazione di report in grado di fornire il contesto necessario per recuperare i dati relativi a ogni cella e valutare quindi l'espressione per ogni cella. Tale client può essere una tabella pivot di Excel o un grafico pivot, un report di Power BI o una query MDX. Indipendentemente dal client di creazione report, viene eseguita una query separata per ogni cella nei risultati. Vale a dire, ogni combinazione di intestazioni di riga e colonna in una tabella pivot o ciascuna selezione di filtri dei dati e filtri in un report di Power BI, genera un subset diverso dei dati su cui viene calcolata la misura. Ad esempio, in una misura con la formula `Total Sales:=SUM([Sales Amount])`, quando un utente inserisce la misura TotalSales nella finestra Values in una tabella pivot, e quindi inserisce la colonna DimProductCategory da una tabella DimProduct nella finestra Filters, la somma di Sales Amount calcolata e visualizzata per ogni categoria di prodotto.  
  
 A differenza delle colonne calcolate e i filtri di riga, la sintassi per una misura include il nome della misura precede la formula. Nell'esempio precedente il nome **Total Sales** viene visualizzato prima della formula. Dopo aver creato una misura, il nome e la relativa definizione vengono visualizzati nell'elenco dei campi dell'applicazione client di creazione di report e, in base alle prospettive e ai ruoli, la misura è disponibile per tutti gli utenti del modello.  
  
 Per altre informazioni, vedere [Misure](../../analysis-services/tabular-models/measures-ssas-tabular.md).  
  
### <a name="row-filters"></a>Filtri di riga  
 I filtri di riga consentono di definire quali righe di una tabella sono visibili ai membri di un particolare ruolo e possono essere creati per ogni tabella in un modello tramite formule DAX. I filtri di riga vengono creati per un particolare ruolo tramite Gestione ruoli in SSDT. I filtri di riga possono anche essere definiti per un modello distribuito tramite le proprietà del ruolo in SQL Server Management Studio (SSMS).  
  
 In un filtro di riga una formula DAX, da cui deve essere restituita una condizione booleana TRUE o FALSE, consente di definire le righe che possono essere restituite dai risultati di una query dei membri di tale particolare ruolo. Non è possibile restituire righe non incluse nella formula DAX. Ad esempio, se nella tabella Customers è presente la seguente formula DAX, `=Customers[Country] = "USA"`, i membri del ruolo relativo alle vendite potranno visualizzare solo i dati relativi ai clienti negli Stati Uniti e le aggregazioni, ad esempio SUM, verranno restituite solo ai clienti negli Stati Uniti.  
  
 Quando si definisce un filtro di riga tramite una formula DAX, si crea un set di righe consentito. Questo non significa che l'accesso alle altre righe viene negato, ma semplicemente che tali righe non vengono restituite come parte del set di righe consentito. Altri ruoli possono consentire l'accesso alle righe escluse dalla formula DAX. Se un utente è membro di un altro ruolo e i filtri di riga del ruolo consentono l'accesso a quel particolare set di righe, l'utente può visualizzare i dati per tale riga.  
  
 I filtri di riga vengono applicati alle righe specificate e a quelle correlate. Quando una tabella dispone di più relazioni, tramite i filtri viene applicata la sicurezza alla relazione che è attiva. I filtri di riga saranno intersecati con altri relativi filtri definiti per le tabelle correlate.  
  
 Per altre informazioni, vedere [ruoli](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
##  <a name="bkmk_DAX_datatypes"></a> Tipi di dati DAX  
 In un modello è possibile importare dati provenienti da numerose origini dati diverse in grado di supportare tipi di dati differenti. Quando si importano dati in un modello, i dati vengono convertiti in uno dei tipi di dati dei modelli tabulari. Quando i dati del modello vengono usati in un calcolo, i dati vengono quindi convertiti in un tipo di dati DAX per la durata e l'output del calcolo. Quando si crea una formula di DAX, i termini utilizzati nella formula determinano automaticamente il tipo di dati del valore restituito.  
  
 I modelli tabulari e DAX supportano i tipi di dati seguenti:  
  
|Tipo di dati nel modello|Tipi di dati in DAX|Descrizione|  
|------------------------|----------------------|-----------------|  
|Numero intero|Valore intero a 64 bit (otto byte) <sup>1, 2</sup>|Numeri senza cifre decimali. I numeri interi possono essere positivi o negativi ma devono essere numeri interi compresi tra -9.223.372.036.854.775.808 (-2^63) e 9.223.372.036.854.775.807 (2^63-1).|  
|Numero decimale|Numero reale a 64 bit (otto byte) <sup>1, 2</sup>|I numeri reali sono numeri che possono avere cifre decimali e coprono un ampio intervallo di valori:<br /><br /> Valori negativi compresi tra -1,79E +308 e -2,23E -308<br /><br /> Zero<br /><br /> Valori positivi compresi tra 2,23E -308 e 1,79E + 308<br /><br /> Tuttavia, il numero di cifre significative è limitato a 17 cifre decimali.|  
|Boolean|Boolean|Valore True o False.|  
|Testo|String|Stringa di dati di tipo carattere Unicode. Può trattarsi di stringhe, numeri o date rappresentati in un formato di testo.|  
|date|Data/ora|Date e ore in una rappresentazione di data e ora valida.<br /><br /> Le date valide sono tutte le date successive al 1 marzo del 1900.|  
|Currency|Currency|Il tipo di dati currency consente valori compresi tra -922.337.203.685.477,5808 e 922.337.203.685.477,5807 con quattro cifre decimali di precisione fissa.|  
|N/D|Vuoto|Un tipo di dati blank in DAX rappresenta e sostituisce i valori Null di SQL. È possibile creare un tipo di dati blank utilizzando la funzione BLANK, nonché verificare la presenza di tipi di dati blank utilizzando la funzione logica ISBLANK.|  
  
 Nei modelli tabulari è inoltre incluso il tipo di dati Table utilizzato come input o output per molte funzioni DAX. Ad esempio, la funzione FILTER consente di utilizzare una tabella come input e di restituire un'altra tabella in cui sono contenute solo le righe che soddisfano le condizioni di filtro. Combinando le funzioni delle tabelle con le funzioni di aggregazione, è possibile eseguire calcoli complessi in set di dati definiti in modo dinamico.  
  
 Anche se i tipi di dati vengono in genere impostati automaticamente, è importante capire i tipi di dati e il modo si applicano, in particolare, alle formule DAX. Gli errori in formule o i risultati imprevisti, ad esempio, sono spesso causati dall'utilizzo di un particolare operatore che non può essere utilizzato con un tipo di dati specificato in un argomento. La formula `= 1 & 2`restituisce, ad esempio, come risultato la stringa 12. La formula `= "1" + "2"`restituisce tuttavia come risultato il valore intero 3.  
  
 Per informazioni dettagliate sui tipi di dati nei modelli tabulari e le conversioni esplicite e implicite di tipi di dati in DAX, vedere [tipi di dati supportati](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md).  
  
##  <a name="bkmk_DAX_opertors"></a> Operatori DAX  
 Nel linguaggio DAX vengono utilizzati quattro tipi diversi di operatori di calcolo nelle formule:  
  
-   Operatori di confronto per confrontare valori e restituire un valore logico TRUE\FALSE.  
  
-   Operatori aritmetici per eseguire calcoli aritmetici che restituiscono valori numerici.  
  
-   Operatori di concatenazione di testo per unire in join due o più stringhe di testo.  
  
-   Operatori logici per combinare due o più espressioni e restituire un singolo risultato.  
  
 Per informazioni dettagliate sugli operatori usati nelle formule DAX, vedere [Guida di riferimento agli operatori DAX](http://msdn.microsoft.com/1befbddc-6178-472c-8bc4-05dafd62207e).  
  
##  <a name="bkmk_DAX_Formulas"></a> Formule DAX  
 Le formule DAX sono essenziali per la creazione di calcoli nelle colonne calcolate e nelle misure e per proteggere i dati tramite filtri a livello di riga. Per creare formule per colonne calcolate e misure, si utilizzerà la barra della formula nella parte superiore della finestra di progettazione modelli o l'Editor DAX. Per creare formule per i filtri di riga, utilizzare la finestra di dialogo Gestione ruoli. Lo scopo delle informazioni fornite in questa sezione è quello di facilitare la comprensione delle nozioni fondamentali relative alle formule DAX.  
  
###  <a name="basics"></a> Nozioni fondamentali sulle formule  
 DAX consente agli autori di modelli tabulari di definire calcoli personalizzati in entrambe le tabelle del modello, come parte di colonne calcolate e come misure associate a tabelle, ma in cui non vengono visualizzati direttamente. DAX consente inoltre agli autori di modelli di proteggere i dati mediante la creazione di calcoli che restituiscono un valore booleano, in base al quale viene definito su quali righe in una tabella particolare o correlata può essere eseguita una query da utenti membri del ruolo associato.  
  
 Le formule DAX possono essere molto semplici o piuttosto complesse. Nella tabella seguente sono riportati alcuni esempi di formule semplici che potrebbero essere utilizzate in una colonna calcolata.  
  
|||  
|-|-|  
|Formula|Descrizione|  
|`=TODAY()`|Consente di inserire la data odierna in ogni riga della colonna.|  
|`=3`|Consente di inserire il valore 3 in ogni riga della colonna.|  
|`=[Column1] + [Column2]`|Consente di sommare i valori nella stessa riga di [Column1] e [Column2] e di inserire i risultati nella colonna calcolata della stessa riga.|  
  
 Per le formule create, sia semplici che complesse, è possibile utilizzare i passaggi seguenti durante la compilazione di una formula:  
  
1.  Ogni formula deve iniziare con un segno di uguale.  
  
2.  È possibile digitare o selezionare il nome di una funzione oppure digitare un'espressione.  
  
3.  Quando si inizia a digitare le prime lettere della funzione o del nome desiderato, la funzionalità Completamento automatico visualizza un elenco di funzioni, tabelle e colonne disponibili. Premere TAB per aggiungere alla formula un elemento dell'elenco Completamento automatico.  
  
     È anche possibile fare clic sul pulsante **Fx** per visualizzare un elenco di funzioni disponibili. Per selezionare una funzione dall'elenco a discesa, utilizzare i tasti di direzione per evidenziare l'elemento, quindi fare clic su **OK** per aggiungere la funzione alla formula.  
  
4.  Fornire gli argomenti per la funzione selezionandoli da un elenco a discesa in cui sono incluse le possibili tabelle e colonne oppure digitando i valori.  
  
5.  Verificare la presenza di errori di sintassi: assicurarsi che tutte le parentesi siano chiuse e che i riferimenti a colonne, tabelle e valori siano corretti.  
  
6.  Premere INVIO per accettare la formula.  
  
> [!NOTE]  
>  In una colonna calcolata, non appena si immette la formula e la formula viene convalidata la colonna viene popolata con i valori. In una misura la relativa definizione misura viene salvata con la tabella nella griglia delle misure premendo INVIO. Se una formula non è valida, verrà visualizzato un errore.  
  
 In questo esempio verrà analizzata una formula più complessa in una misura denominata Days in Current Quarter:  
  
```  
Days in Current Quarter:=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))  
```  
  
 Questa misura viene utilizzata per creare un rapporto di confronto tra un periodo incompleto e il periodo precedente. È necessario che nella formula la proporzione del periodo trascorso venga presa in considerazione e confrontata con la stessa proporzione del periodo precedente. In questo caso, [Days Current Quarter to Date]/[Days in Current Quarter] fornisce la proporzione trascorsa nel periodo corrente.  
  
 Questa formula contiene i seguenti elementi:  
  
|Elemento della formula|Descrizione|  
|---------------------|-----------------|  
|`Days in Current Quarter:=`|Nome della misura.|  
|`=`|Il segno di uguale (=) inizia la formula.|  
|`COUNTROWS`|La [funzione COUNTROWS (DAX)](http://msdn.microsoft.com/830dd659-5405-4e0a-8d26-01ae9d5e5e9a) conta il numero totale di righe nella tabella Date.|  
|`()`|Le parentesi di apertura e chiusura specificano gli argomenti.|  
|`DATESBETWEEN`|La funzione DATESBETWEEN restituisce le date tra l'ultima data per ogni valore nella colonna Date della tabella Date.|  
|`'Date'`|Specifica la tabella Date. Le tabelle sono racchiuse tra virgolette singole.|  
|`[Date]`|Specifica la colonna Date nella tabella Date. Le colonne sono racchiuse tra parentesi.|  
|`,`||  
|`STARTOFQUARTER`|La funzione STARTOFQUARTER restituisce la data dell'inizio del trimestre.|  
|`LASTDATE`|La funzione LASTDATE restituisce l'ultima data del trimestre.|  
|`'Date'`|Specifica la tabella Date.|  
|`[Date]`|Specifica la colonna Date nella tabella Date.|  
|`,`||  
|`ENDOFQUARTER`|Funzione ENDOFQUARTER|  
|`'Date'`|Specifica la tabella Date.|  
|`[Date]`|Specifica la colonna Date nella tabella Date.|  
  
#### <a name="using-formula-autocomplete"></a>Utilizzo di Completamento automatico formule  
 Sia nella barra della formula in Progettazione modelli che nella finestra dei filtri di riga della formula nella finestra di dialogo Gestione ruoli è disponibile una funzionalità di completamento automatico, che consente di immettere una sintassi della formula valida visualizzando le opzioni per ogni elemento della formula.  
  
-   È possibile utilizzare Completamento automatico formule in una formula esistente con funzioni nidificate. Il testo immediatamente prima del punto di inserimento viene utilizzato per visualizzare i valori nell'elenco a discesa mentre tutto il testo dopo tale punto rimane invariato.  
  
-   In Completamento automatico non viene aggiunta la parentesi di chiusura delle funzioni né vengono inserite automaticamente le parentesi corrispondenti. È necessario assicurarsi che ogni funzione sia sintatticamente corretta, altrimenti non sarà possibile salvare o utilizzare la formula.  
  
#### <a name="using-multiple-functions-in-a-formula"></a>Utilizzo di più funzioni in una formula  
 È possibile nidificare funzioni, pertanto è possibile utilizzare i risultati di una funzione come argomento di un'altra funzione. È possibile annidare fino a 64 livelli di funzioni nelle colonne calcolate. La nidificazione può tuttavia rendere più complessa la creazione di formule o la risoluzione dei problemi relativi alle formule.  
  
 Numerose funzioni sono progettate per essere utilizzate esclusivamente come funzioni nidificate. Tramite queste funzioni viene restituita una tabella, che non può essere salvata direttamente come risultato, ma deve essere fornita come input per una funzione di tabella. Ad esempio, per le funzioni SUMX, AVERAGEX e MINX è richiesta una tabella come primo argomento.  
  
> [!NOTE]  
>  Vengono applicati alcuni limiti alla nidificazione di funzioni all'interno delle misure, per assicurare che le prestazioni non vengano compromesse dai numerosi calcoli richiesti dalle dipendenze tra colonne.  
  
##  <a name="bkmk_DAX_functions"></a> Funzioni DAX  
 In questa sezione viene fornita una panoramica dei *tipi* di funzioni supportati nel linguaggio DAX. Per altre informazioni dettagliate, vedere [Riferimento alle funzioni DAX](http://msdn.microsoft.com/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
 In DAX è disponibile una varietà di funzioni che è possibile utilizzare per eseguire calcoli basati su date e ore, creare valori condizionali, utilizzare stringhe, eseguire ricerche basate sulle relazioni, nonché la possibilità di eseguire l'iterazione di una tabella per l'esecuzione di calcoli ricorsivi. Se si ha dimestichezza con le formule di Excel, molte di queste funzioni appariranno molto simili, tuttavia, le formule DAX sono diverse nelle seguenti modalità importanti:  
  
-   Una funzione DAX fa sempre riferimento a una colonna completa o una tabella. Se si desidera utilizzare solo particolari valori di una tabella o colonna, è possibile aggiungere filtri alla formula.  
  
-   Se è necessario personalizzare i calcoli per ogni singola riga, in DAX sono disponibili funzioni che consentono di utilizzare il valore della riga corrente o un valore correlato come un tipo di parametro, per eseguire i calcoli che variano in base al contesto. Per comprendere l'utilizzo di queste funzioni, vedere [Context in DAX Formulas](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md#bkmk_context) più avanti in questo argomento.  
  
-   In DAX sono incluse molte funzioni mediante le quali viene restituita una tabella, anziché un valore. La tabella non viene visualizzata in uno strumento client di creazione report, ma viene utilizzata per fornire input ad altre funzioni. Ad esempio, è possibile recuperare una tabella e contare i valori distinti in essa contenuti o calcolare somme dinamiche nelle tabelle o colonne filtrate.  
  
-   Funzioni DAX sono incluse numerose *business intelligence* funzioni. Queste funzioni consentono di definire o selezionare intervalli di date e di eseguire calcoli dinamici in base a tali date o intervalli. Ad esempio, è possibile confrontare somme in periodi paralleli.  
  
### <a name="date-and-time-functions"></a>Funzioni di data e ora  
 Le funzioni di data e ora in DAX sono molto simili alle funzioni di data e ora di Microsoft Excel. Le funzioni DAX sono tuttavia basate sui tipi di dati **datetime** utilizzati da Microsoft SQL Server. Per altre informazioni, vedere [Funzioni di data e ora (DAX)](http://msdn.microsoft.com/9fc9214a-fcd6-40c0-bf51-0c95637c6ffb).  
  
### <a name="filter-functions"></a>Funzioni di filtro  
 Le funzioni di filtro in DAX restituiscono specifici tipi di dati, cercano valori nelle tabelle correlate e filtrano in base a valori correlati. Le funzioni di ricerca utilizzano tabelle e relazioni, come un database. Le funzioni di filtro consentono di modificare il contesto dei dati per creare calcoli dinamici. Per altre informazioni, vedere [Funzioni filtro (DAX)](http://msdn.microsoft.com/b036fd40-4d3b-426d-a0d2-80258b53d8e5).  
  
### <a name="information-functions"></a>Funzioni informative  
 Una funzione informativa analizza la cella o la riga fornita come argomento e indica se il valore corrisponde al tipo previsto. La funzione ISERROR, ad esempio, restituisce TRUE se il valore a cui si fa riferimento contiene un errore. Per altre informazioni, vedere [Funzioni informative (DAX)](http://msdn.microsoft.com/6d2bee09-0456-4444-b4d2-c231fd788a2e).  
  
### <a name="logical-functions"></a>Funzioni logiche  
 Le funzioni logiche eseguono operazioni su un'espressione per restituire informazioni sui valori nell'espressione. La funzione TRUE, ad esempio, consente di sapere se un'espressione che si sta valutando restituirà un valore TRUE. Per altre informazioni, vedere [Funzioni logiche (DAX)](http://msdn.microsoft.com/2eb33add-60b2-44ab-b761-012a473116a2).  
  
### <a name="mathematical-and-trigonometric-functions"></a>Funzioni matematiche e trigonometriche  
 Le funzioni matematiche in DAX sono molto simili alle funzioni matematiche e trigonometriche di Excel. Esistono tuttavia alcune piccole differenze nei tipi di dati numerici utilizzati dalle funzioni DAX. Per altre informazioni, vedere [Funzioni matematiche e trigonometriche (DAX)](http://msdn.microsoft.com/1f408ec1-e769-43d6-a68c-567bc30d893f).  
 
### <a name="other-functions"></a>Altre funzioni  
 Queste funzioni eseguono azioni univoche che non possono essere definite da una qualsiasi delle categorie a che la maggior parte delle altre funzioni appartengono. Per altre informazioni, vedere [altre funzioni (DAX)](https://msdn.microsoft.com/mt150101).
  
### <a name="statistical-functions"></a>Funzioni statistiche  
 In DAX sono disponibili funzioni statistiche per l'esecuzione di aggregazioni. Oltre a creare somme e medie o a trovare valori minimi e massimi, in DAX è anche possibile filtrare una colonna prima di aggregare o creare aggregazioni in base a tabelle correlate. Per altre informazioni, vedere [Funzioni statistiche (DAX)](http://msdn.microsoft.com/ba4c1298-57a0-40fc-b6f6-00e187ace559).  
  
### <a name="text-functions"></a>Funzioni di testo  
 Le funzioni di testo in DAX sono molto simili alle funzioni corrispondenti in Excel. È possibile restituire parte di una stringa, cercare testo all'interno di una stringa o concatenare valori stringa. In DAX sono inoltre disponibili funzioni per il controllo dei formati per date, ore e numeri. Per altre informazioni, vedere [Funzioni di testo (DAX)](http://msdn.microsoft.com/e4821571-ae55-4df7-ae98-c578200bba5f).  
  
### <a name="time-intelligence-functions"></a>Funzioni di business intelligence  
 Le funzioni di business intelligence fornite in DAX consentono di creare calcoli che utilizzano informazioni predefinite su calendari e date. Tramite gli intervalli di ore e date in combinazione con aggregazioni o calcoli è possibile compilare confronti significativi tra periodi di tempo paragonabili relativamente a vendite, scorte e così via. Per altre informazioni, vedere [funzioni di business intelligence (DAX)](http://msdn.microsoft.com/91df278d-4b28-40c1-a572-cdb91f081517).  
  
###  <a name="bkmk_TableFunc"></a> Funzioni con valori di tabella  
 Sono disponibili funzioni DAX che consentono di eseguire l'output di tabelle, che utilizzano le tabelle come input o che svolgono entrambe le funzioni. Dal momento che una tabella può disporre di una sola colonna, le funzioni con valori di tabella utilizzano anche le singole colonne come input. Saper utilizzare tali funzioni con valori di tabella è importante per un utilizzo ottimale delle formule DAX. DAX include i seguenti tipi di funzioni con valori di tabella:  
  
  **Funzioni di filtro** -restituiscono una colonna, tabella o valori correlati alla riga corrente.  
    
  **Funzioni di aggregazione** -aggregano qualsiasi espressione nelle righe di una tabella.  
    
  **Funzioni di business intelligence** : restituire una tabella di date o utilizzano una tabella di date per calcolare un'aggregazione.  
  
##  <a name="bkmk_context"></a> Contesto nelle formule DAX  
 Il*contesto* è un concetto importante da comprendere in caso di creazione di formule tramite DAX. Rappresenta l'elemento che consente di eseguire analisi dinamiche, dal momento che i risultati di una formula vengono modificati per riflettere la riga o la selezione della cella corrente, nonché anche eventuali dati correlati. La comprensione del contesto e l'utilizzo efficace di quest'ultimo sono fondamentali per la realizzazioni di analisi dinamiche ad elevate prestazioni e per la risoluzione dei problemi riscontrati nelle formule.  
  
 Le formule nei modelli tabulari possono essere valutate in un contesto diverso, in base ad altri elementi di progettazione quali:  
  
-   Filtri applicati in una tabella pivot o in un report  
  
-   Filtri definiti all'interno di una formula  
  
-   Relazioni specificate tramite funzioni speciali all'interno di una formula  
  
 Esistono diversi tipi di contesto: *contesto di riga*, *contesto di query*e *contesto di filtro*.  
  
###  <a name="bkmk_row_context"></a> Contesto di riga  
 *Contesto di riga* può essere considerato la "riga corrente". Se si crea una formula in una colonna calcolata, nel contesto di riga per tale formula sono inclusi i valori di tutte le colonne presenti nella riga corrente. Se la tabella è correlata a un'altra tabella, il contenuto include anche tutti i valori dell'altra tabella che sono correlati alla riga corrente.  
  
 Si supponga ad esempio di creare una colonna calcolata, `=[Freight] + [Tax]`, in cui vengono sommati i valori di due colonne, Freight e Tax, della stessa tabella. Tramite questa formula si ottengono automaticamente solo i valori dalla riga corrente delle colonne specificate.  
  
 Il contesto di riga segue inoltre qualsiasi relazione definita tra le tabelle, incluse le relazioni definite all'interno di una colonna calcolata tramite formule DAX, per determinare quali righe nelle tabelle correlate sono associate alla riga corrente.  
  
 Nella formula seguente viene ad esempio utilizzata la funzione RELATED per recuperare un valore relativo all'imposta da una tabella correlata, in base all'area in cui è stato eseguito l'ordine. Il valore dell'imposta viene determinato utilizzando il valore per regione nella tabella corrente, effettuando la ricerca della regione nella tabella correlata e quindi ottenendo l'aliquota di imposta per tale regione dalla tabella correlata.  
  
```  
= [Freight] + RELATED('Region'[TaxRate])  
```  
  
 Questa formula ottiene l'aliquota di imposta per la regione corrente dalla tabella Region e la somma al valore della colonna Freight. Nelle formule DAX non è necessario conoscere o specificare la relazione specifica che connette le tabelle.  
  
#### <a name="multiple-row-context"></a>Contesto di più righe  
 In DAX sono inoltre incluse funzioni che iterano i calcoli in una tabella. Queste funzioni possono presentare più righe correnti, ognuna con un proprio contesto di riga.  In pratica, queste funzioni consentono di creare formule mediante le quali vengono eseguite operazioni in modo ricorsivo su un ciclo interno ed esterno.  
  
 Si supponga ad esempio che in un modello sia contenuta una tabella **Products** e una tabella **Sales** . Potrebbe essere necessario scorrere l'intera tabella delle vendite, piena di transazioni che riguardano più prodotti, e individuare la quantità più grande ordinata per ogni prodotto in una transazione qualunque.  
  
 Con DAX è possibile compilare una sola formula mediante la quale viene restituito il valore corretto e i risultati vengono aggiornati automaticamente tutte le volte che un utente aggiunge dati alle tabelle.  
  
```  
=MAXX(FILTER(Sales,[ProdKey]=EARLIER([ProdKey])),Sales[OrderQty])  
```  
  
 Per una procedura dettagliata di questa formula, vedere [Funzione EARLIER (DAX)](http://msdn.microsoft.com/6d126c4d-2315-49ec-899d-cb396eefbae6).  
  
 Per riepilogare, la funzione EARLIER consente di archiviare il contesto di riga dall'operazione che ha preceduto l'operazione corrente. La funzione archivia sempre in memoria due set di contesto: uno rappresenta la riga corrente del ciclo interno della formula e l'altro rappresenta la riga corrente del ciclo esterno della formula. DAX utilizza automaticamente i valori tra due cicli in modo che sia possibile creare aggregazioni complesse.  
  
####  <a name="bkmk_query_context"></a> Contesto di query  
 Il*contesto di query* fa riferimento al subset di dati recuperato in modo implicito per una formula. Quando un utente inserisce una misura o un altro campo valori in una tabella pivot o in un report basato su un modello tabulare, tramite il motore vengono esaminate le intestazioni di riga e di colonna, i filtri dei dati e i filtri dei report per determinare il contesto. Le query necessarie vengono quindi eseguite sull'origine dati per ottenere il subset corretto di dati, effettuare i calcoli definiti dalla formula e popolare ogni cella nella tabella pivot o nel report. Il set di dati recuperato è il contesto di query per ogni cella.  
  
> [!WARNING]  
>  Per un modello in modalità DirectQuery, viene valutato il contesto e, successivamente, le operazioni di impostazione per recuperare il subset corretto di dati e calcolare i risultati vengono convertite in istruzioni SQL. Tali istruzioni vengono quindi eseguite direttamente sull'archivio dati relazionale. Pertanto, anche se il metodo di acquisizione dei dati e di calcolo dei risultati è diverso, il contesto stesso non viene modificato.  
  
 Dal momento che il contesto cambia a seconda della posizione della formula, anche i risultati della formula possono cambiare.  
  
 Si supponga ad esempio di creare una formula in cui vengono sommati i valori della colonna **Profit** della tabella **Sales** : `=SUM('Sales'[Profit])`.  Se si utilizza tale formula in una colonna calcolata all'interno della tabella **Sales** , i risultati saranno uguali per l'intera tabella, in quanto il contesto di query per la formula è sempre l'intero set di dati della tabella **Sales** . I risultati indicheranno i profitti per tutte le regioni, tutti i prodotti, tutti gli anni e così via.  
  
 In genere, non è tuttavia necessario visualizzare lo stesso risultato centinaia di volte, poiché è più utile ottenere i profitti per un anno, un paese, un prodotto specifico o una combinazione di tali elementi, per pervenire quindi a un totale complessivo.  
  
 In una tabella pivot è possibile modificare il contesto aggiungendo o rimuovendo intestazioni di colonna e di riga, nonché aggiungendo o rimuovendo filtri dei dati. Ogni qualvolta si aggiungono intestazioni di riga o di colonna alla tabella pivot, si modifica il contesto di query nel quale viene valutata la misura. Anche le operazioni di applicazione di filtri influiscono sul contesto. Pertanto, la stessa formula utilizzata in una misura viene valutata in un *contesto di query* diverso per ogni cella.  
  
####  <a name="bkmk_filter_context"></a> Contesto di filtro  
 Il*contesto di filtro* è il set di valori consentito in ogni colonna o nei valori recuperati da una tabella correlata. I filtri possono essere applicati alla colonna nella finestra di progettazione o nel livello di presentazione (report e tabelle pivot). Possono essere definiti inoltre in modo esplicito dalle espressioni di filtro all'interno della formula.  
  
 Il contesto di filtro viene aggiunto quando si specificano vincoli del filtro sul set di valori consentito in una colonna o una tabella utilizzando gli argomenti di una formula. Tale contesto viene applicato su altri contesti, ad esempio il contesto di riga o il contesto di query.  
  
 Nei modelli tabulari sono disponibili molti modi per creare il contesto di filtro. All'interno del contesto di client che possono utilizzare il modello, ad esempio report di Power BI, gli utenti possono creare filtri immediatamente aggiungendo filtri dei dati o filtri report sulle intestazioni di riga e colonna. È possibile specificare anche espressioni di filtro direttamente all'interno della formula, per specificare i valori correlati, per filtrare tabelle utilizzate come input o per ottenere dinamicamente il contesto per i valori utilizzati nei calcoli. È inoltre possibile deselezionare completamente o in modo selettivo i filtri in colonne specifiche. Questa operazione risulta molto utile quando si creano formule che consentono di calcolare totali complessivi.  
  
 Per altre informazioni sulla creazione di filtri nelle formule, vedere [Funzione FILTER (DAX)](http://msdn.microsoft.com/f1f6bee4-547b-407c-b70b-9216b2f3d3fd).  
  
 Per un esempio della modalità di deselezione dei filtri per creare totali complessivi, vedere [Funzione ALL (DAX)](http://msdn.microsoft.com/a7e0ab71-d83e-4463-bc77-9eb5dd73c6fc).  
  
 Per esempi di deselezione e applicazione di filtri in modo selettivo all'interno di formule, vedere [Funzione ALLEXCEPT (DAX)](http://msdn.microsoft.com/a6f575a1-9803-4bb2-85b3-c95c060f1fb1).  
  
####  <a name="bkmk_determine_context"></a> Determinazione del contesto nelle formule  
 Una volta creata una formula DAX, viene innanzitutto testata la validità della relativa sintassi e viene quindi verificato che i nomi delle colonne e delle tabelle incluse nella formula siano presenti nel contesto corrente. Se non è possibile trovare una colonna o una tabella specificata dalla formula, viene restituito un errore.  
  
 Il contesto durante la convalida, e le operazioni di ricalcolo, viene determinato come descritto nelle sezioni precedenti utilizzando le tabelle disponibili nel modello, eventuali relazioni tra le tabelle ed eventuali filtri applicati.  
  
 Se ad esempio sono appena stati importati dati in una nuova tabella che non sono correlati a nessun'altra e a cui non è stato applicato alcun filtro, il *contesto corrente* è tutto il set di colonne della tabella. Se la tabella è collegata tramite relazioni ad altre tabelle, nel contesto corrente sono incluse le tabelle correlate. Se si aggiunge una colonna della tabella a un report che dispone di filtri dei dati e forse di alcuni filtri report, il contesto per la formula è il subset di dati in ogni cella del report.  
  
 Quello di contesto è un concetto articolato e complesso, che può rendere difficile risolvere i problemi relativi alle formule. È consigliabile iniziare con formule e relazioni semplici per verificare il funzionamento del contesto. Nella sezione seguente vengono forniti alcuni esempi del modo in cui le formule utilizzano tipi diversi di contesto per restituire risultati in modo dinamico.  
  
##### <a name="examples-of-context-in-formulas"></a>Esempi di contesto nelle formule  
  
1.  La [funzione RELATED (DAX)](http://msdn.microsoft.com/0023fd13-c17a-4243-ab77-3779a4b502b6) espande il contesto della riga corrente per includere i valori di una colonna correlata. Ciò consente di eseguire ricerche. Nell'esempio di questo argomento viene illustrata l'interazione del contesto di filtro e del contesto di riga.  
  
2.  La [funzione FILTER (DAX)](http://msdn.microsoft.com/f1f6bee4-547b-407c-b70b-9216b2f3d3fd) consente di specificare le righe da includere nel contesto corrente. Negli esempi di questo argomento viene inoltre illustrato come incorporare filtri in altre funzioni che eseguono aggregazioni.  
  
3.  La [funzione ALL (DAX)](http://msdn.microsoft.com/a7e0ab71-d83e-4463-bc77-9eb5dd73c6fc) imposta il contesto all'interno di una formula. È possibile utilizzarla per eseguire l'override dei filtri applicati come risultato del contesto di query.  
  
4.  La [funzione ALLEXCEPT(DAX)](http://msdn.microsoft.com/a6f575a1-9803-4bb2-85b3-c95c060f1fb1) consente di rimuovere tutti i filtri, ad eccezione di quello specificato. In entrambi gli argomenti sono inclusi esempi che illustrano la compilazione di formule e forniscono informazioni sui contesti complessi.  
  
5.  Le funzioni [EARLIER (DAX)](http://msdn.microsoft.com/6d126c4d-2315-49ec-899d-cb396eefbae6) e [EARLIEST (DAX)](http://msdn.microsoft.com/9befa04d-78db-492e-a463-80b8b77206d6) consentono di eseguire il ciclo in tabelle mediante l'esecuzione di calcoli, facendo riferimento nel contempo a un valore proveniente da un ciclo interno. Se si ha familiarità con il concetto di ricorsione e con i cicli interni ed esterni, sarà più facile apprezzare l'efficacia offerta dalle funzioni EARLIER ed EARLIEST. Se non si ha familiarità con tali concetti, è opportuno seguire con attenzione i passaggi nell'esempio per informazioni sulle modalità di utilizzo dei contesti interni ed esterni nell'esecuzione di calcoli.  
  
##  <a name="bkmk_RelModel"></a> Formule e modello tabulare  
 Progettazione modelli, in SSDT, è un'area in cui è possibile utilizzare più tabelle di dati e connettere le tabelle in un modello tabulare. All'interno di questo modello le tabelle sono unite da relazioni in colonne con valori (chiavi) comuni. Il modello tabulare consente di collegare valori a colonne di altre tabelle e creare calcoli più interessanti. Analogamente a un database relazionale, è possibile collegare molti livelli di tabelle correlate e utilizzare colonne di qualsiasi tabella nei risultati.  
  
 È possibile collegare ad esempio una tabella delle vendite, una tabella dei prodotti e una tabella delle categorie di prodotto e utilizzare le varie combinazioni delle colonne delle tabelle pivot e dei report. I campi correlati possono essere utilizzati per filtrare tabelle connesse o per creare calcoli in subset. (Se non ha familiarità con i database relazionale e utilizzo delle tabelle e join, vedere [relazioni](../../analysis-services/tabular-models/relationships-ssas-tabular.md).)  
  
 I modelli tabulari supportano più relazioni tra tabelle. Per evitare confusione o risultati errati, viene definita come relazione attiva solo una relazione per volta. Tuttavia, è possibile modificare la relazione attiva, se necessario, per attraversare connessioni diverse nei dati nei calcoli. La [funzione USERELATIONSHIP (DAX)](http://msdn.microsoft.com/200484ab-9da1-4570-a100-7f9ed20d33af) può essere usata per specificare una o più relazioni da usare in un calcolo specifico.  
  
 In un modello tabulare è necessario osservare le seguenti regole di progettazione delle formule:  
  
-   Quando le tabelle sono connesse tramite una relazione, è necessario assicurarsi che le due colonne utilizzate come chiavi dispongano di valori corrispondenti. L'integrità referenziale non viene tuttavia applicata, pertanto è possibile che in una colonna chiave siano presenti valori non corrispondenti, ma che si possa comunque creare una relazione. In tal caso, è necessario tenere presente che i valori vuoti o non corrispondenti potrebbero influire sui risultati delle formule.  
  
-   Quando si collegano tabelle nel modello tramite relazioni, viene ampliato l'ambito o *contesto*nel quale vengono valutate le formule. Le modifiche al contesto che derivano dall'aggiunta di nuove tabelle, di nuove relazioni o da cambiamenti della relazione attiva possono causare modiche ai risultati difficili da prevedere. Per altre informazioni, vedere [Contesto nelle formule DAX](#bkmk_context) più avanti in questo argomento.  
  
##  <a name="bkmk_tables"></a> Utilizzo di tabelle e colonne  
 Le tabelle nei modelli tabulari sono simili a quelle di Excel, ma differiscono nell'utilizzo dei dati e delle formule:  
  
-   Nelle formule vengono utilizzate solo tabelle e colonne, non celle singole, riferimenti a intervalli o matrici.  
  
-   Nelle formule possono essere utilizzate relazioni per ottenere i valori dalle tabelle correlate. I valori recuperati sono sempre correlati al valore della riga corrente.  
  
-   Non è possibile avere dati irregolari o non allineati come in un foglio di lavoro di Excel. Ogni riga di una tabella deve contenere lo stesso numero di colonne. Tuttavia è possibile disporre di valori vuoti in alcune colonne. Le tabelle di dati di Excel e quelle dei modelli tabulari non sono intercambiabili.  
  
-   Poiché per ogni colonna viene impostato un tipo di dati, ogni valore nella colonna deve essere dello stesso tipo.  
  
### <a name="referring-to-tables-and-columns-in-formulas"></a>Riferimento a tabelle e colonne nelle formule  
 È possibile fare riferimento a qualsiasi tabella e colonna tramite il relativo nome. Ad esempio, nella formula seguente viene illustrato come fare riferimento alle colonne da due tabelle utilizzando il nome *completo* :  
  
```  
=SUM('New Sales'[Amount]) + SUM('Past Sales'[Amount])  
```  
  
 Durante la valutazione di una formula, in Progettazione modelli viene verificata prima la sintassi generale, quindi vengono controllati i nomi delle colonne e delle tabelle forniti in base alle possibili colonne e tabelle del contesto corrente. Se il nome è ambiguo o non è possibile trovare la colonna o tabella, si verificherà un errore nella formula e nelle celle in cui si è verificato l'errore verrà visualizzata una stringa #ERRORE anziché il valore di dati. Per altre informazioni sui requisiti per la denominazione di tabelle, colonne e altri oggetti, vedere la sezione "Requisiti per la denominazione" in [Specifica della sintassi DAX](http://msdn.microsoft.com/098630f4-7d1d-467e-976c-99b2279430d5).  
  
### <a name="table-relationships"></a>Relazioni tra tabelle  
 La creazione di relazioni tra le tabelle consente di eseguire ricerche di dati in un'altra tabella e di utilizzare i valori correlati per eseguire calcoli complessi. Ad esempio, è possibile utilizzare una colonna calcolata per individuare tutti i record di spedizione correlati al rivenditore corrente, quindi sommare i costi di spedizione per ognuno di essi. In molti casi, tuttavia, una relazione potrebbe non essere necessaria. È possibile usare la funzione LOOKUPVALUE in una formula per restituire il valore in *result_columnName* per la riga che soddisfa i criteri specificati nei parametri *search_column* e *search_value* .  
  
 Molte funzioni DAX richiedono l'esistenza di una relazione tra le tabelle, o tra più tabelle, per consentire l'individuazione delle colonne cui è stato fatto riferimento e restituire risultati appropriati. Tramite altre funzioni verrà tentata l'identificazione della relazione, tuttavia per ottenere i migliori risultati è consigliabile creare sempre una relazione dove possibile. Per altre informazioni, vedere [Formule e modello tabulare](#bkmk_RelModel) più indietro in questo argomento.  
  
##  <a name="bkmk_RefreshRecalc"></a> Aggiornamento dei risultati delle formule (elaborazione)  
 L'*elaborazione dei dati* e il *ricalcolo* sono due operazioni distinte ma correlate. È necessario comprendere in modo approfondito questi concetti ai fini della progettazione di un modello contenente formule complesse, grandi quantità di dati o dati ottenuti da origini dati esterne.  
  
 L'*aggiornamento dei dati* è il processo di aggiornamento dei dati in un modello con nuovi dati provenienti da un'origine dati esterna.  
  
 Il*ricalcolo* è il processo di aggiornamento dei risultati delle formule in modo che riflettano qualsiasi modifica alle formule stesse e le modifiche nei dati sottostanti. Il ricalcolo può avere effetto sulle prestazioni nei modi seguenti:  
  
-   I valori in una colonna calcolata vengono calcolati e archiviati nel modello. Per aggiornare i valori nella colonna calcolata, è necessario elaborare il modello usando uno dei tre comandi di elaborazione - processo completo, elaborazione dei dati o Elabora ricalcolo. È necessario sempre ricalcolare il risultato della formula per la colonna intera, ogni volta che la formula viene modificata.  
  
-   I valori calcolati dalle misure vengono valutati dinamicamente ogni volta che un utente aggiunge la misura a una tabella pivot o apre un report; quando l'utente modifica il contesto, i valori restituiti dalla misura vengono modificati di conseguenza. I risultati della misura riflettono sempre gli ultimi dati nella cache in memoria.  
  
 L'elaborazione e il ricalcolo non hanno effetto sulle formule del filtro di riga, a meno che il risultato di un ricalcolo restituisca un valore diverso, rendendo in tal modo possibile o impedendo l'esecuzione di query sulla riga da parte di membri del ruolo.  
  
 Per altre informazioni, vedere [Processdataaccess](../../analysis-services/tabular-models/process-data-ssas-tabular.md).  
  
##  <a name="bkmk_troubleshoot"></a> Risoluzione degli errori nelle formule  
 Se si ottiene un errore quando si definisce una formula, è possibile che la formula contenga un *errore sintattico*, un *errore semantico*o un *errore di calcolo*.  
  
 Gli errori sintattici sono i più facili da risolvere. In genere sono dovuti a una parentesi o una virgola mancante. Per informazioni sulla sintassi delle singole funzioni, vedere [Riferimento alle funzioni DAX](http://msdn.microsoft.com/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
 L'altro tipo di errore si verifica quando la sintassi è corretta, ma il valore o la colonna a cui si fa riferimento non è appropriato nel contesto della formula. Tali errori semantici e di calcolo potrebbero essere causati da uno qualsiasi dei problemi seguenti:  
  
-   La formula fa riferimento a una colonna, una tabella o una funzione non esistente.  
  
-   La formula sembra essere corretta, ma quando tramite il motore dei dati vengono recuperati i dati, viene rilevato un tipo non corrispondente e quindi generato un errore.  
  
-   La formula passa a una funzione un numero o un tipo di parametro errato.  
  
-   La formula fa riferimento a una colonna diversa che contiene un errore e pertanto i valori non sono validi.  
  
-   La formula fa riferimento a una colonna che non è stata elaborata, pertanto dispone di metadati ma non dati effettivi da utilizzare per i calcoli.  
  
 Nei primi quattro casi, tramite DAX viene contrassegnata l'intera colonna in cui è contenuta la formula non valida. Nell'ultimo caso, tramite DAX la colonna che si trova in uno stato non elaborato viene visualizzata in grigio.  
  
##  <a name="bkmk_addional_resources"></a> Risorse aggiuntive  
 In [Modellazione tabulare &#40;esercitazione di AdventureWorks&#41;](../../analysis-services/tabular-modeling-adventure-works-tutorial.md) vengono fornite istruzioni dettagliate sulla creazione di un modello tabulare che include molti calcoli in colonne calcolate, misure e filtri di riga. Per la maggior parte delle formule viene fornita una descrizione dello scopo della formula.  
  
 Il [blog del Team di Analysis Services](http://go.microsoft.com/fwlink/?LinkID=220949&clcid=0x409) fornisce informazioni aggiornate, suggerimenti, notizie e annunci. 
  
 In [Centro risorse di DAX](http://go.microsoft.com/fwlink/?LinkID=220966&clcid=0x409) vengono fornite informazioni interne ed esterne su DAX, incluse numerose soluzioni DAX inviate da noti professionisti di Business Intelligence.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento a Data Analysis Expressions (DAX)](http://msdn.microsoft.com/70a82136-0926-4a91-bcb3-e18e82593b0d)   
 [Misure](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Colonne calcolate](../../analysis-services/tabular-models/ssas-calculated-columns.md)   
 [Ruoli](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [Indicatori KPI](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Origini dati supportate](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
