---
title: Relazioni (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 21e0144a-3cfd-4bc7-87ff-bb7d1800ed2f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a0a1527ed97570c715ff383837ebd5a9d5a3354
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66066695"
---
# <a name="relationships-ssas-tabular"></a>Relazioni (SSAS tabulare)
  Nei modelli tabulari, una relazione è una connessione tra due tabelle di dati e consente di stabilire in che modo devono essere correlati i dati nelle due tabelle. È ad esempio possibile mettere in correlazione una tabella Clienti e una tabella Ordini per mostrare il nome del cliente associato a ciascun ordine.  
  
 Se si utilizza l'Importazione guidata tabella per importare dalla stessa origine dati, le relazioni già presenti nelle tabelle (a livello di origine dati) che si sceglie di importare saranno ricreate nel modello. È possibile visualizzare le relazioni rilevate e ricreate automaticamente tramite Progettazione modelli nella Vista diagramma o la finestra di dialogo Gestisci relazioni. È inoltre possibile creare manualmente nuove relazioni tra tabelle tramite Progettazione modelli nella Vista diagramma o la finestra di dialogo Crea relazione o Gestisci relazioni.  
  
 Dopo avere definito relazioni tra tabelle, in modo automatico durante l'importazione o in modo manuale, sarà possibile filtrare i dati utilizzando colonne correlate e cercare valori nelle tabelle correlate.  
  
> [!TIP]  
>  Se il modello contiene molte relazioni, la Vista diagramma consente di creare nuove relazioni tra tabelle e di visualizzarle meglio.  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#what)  
  
-   [Requisiti per le relazioni](#requirements)  
  
-   [Inferenza delle relazioni](#detection)  
  
-   [Rilevamento di relazioni durante l'importazione di dati](#bkmk_detection)  
  
-   [Creazione manuale di relazioni](#bkmk_manually_create)  
  
-   [Valori duplicati e altri errori](#bkmk_dupl_errors)  
  
-   [Attività correlate](#bkmk_related_tasks)  
  
##  <a name="benefits"></a><a name="what"></a>Vantaggi  
 Una relazione è una connessione tra due tabelle di dati, in base a una o più colonne in ogni tabella. Per capire perché le relazioni sono utili, provare a immaginare di tenere traccia degli ordini di un cliente della propria azienda. È possibile tenere traccia di tutti i dati in un'unica tabella che dispone di una struttura simile alla seguente:  
  
|CustomerID|Nome|EMail|DiscountRate|OrderID|OrderDate|Prodotto|Quantità|  
|----------------|----------|-----------|------------------|-------------|---------------|-------------|--------------|  
|1|Ashton|chris.ashton@contoso.com|.05|256|07/01/2010|Compact Digital|11|  
|1|Ashton|chris.ashton@contoso.com|.05|255|03/01/2010|SLR Camera|15|  
|2|Jaworski|michal.jaworski@contoso.com|0,10|254|03/01/2010|Budget Movie-Maker|27|  
  
 Questo approccio può funzionare, tuttavia comporta l'archiviazione di molti dati ridondanti, ad esempio l'indirizzo di posta elettronica del cliente per ogni ordine. L'archiviazione è economica ma è necessario assicurarsi di aggiornare ogni riga relativa al cliente nel caso in cui l'indirizzo di posta elettronica cambi. Una soluzione a questo problema è suddividere i dati in più tabelle e definire relazioni tra tali tabelle. Si tratta dell'approccio usato nei *database relazionali* come [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ad esempio, un database importato in un modello potrebbe rappresentare i dati dell'ordine tramite tre tabelle correlate:  
  
### <a name="customers"></a>Clienti  
  
|[CustomerID]|Nome|Posta elettronica|  
|--------------------|----------|-----------|  
|1|Ashton|chris.ashton@contoso.com|  
|2|Jaworski|michal.jaworski@contoso.com|  
  
### <a name="customerdiscounts"></a>CustomerDiscounts  
  
|[CustomerID]|DiscountRate|  
|--------------------|------------------|  
|1|.05|  
|2|0,10|  
  
### <a name="orders"></a>Orders  
  
|[CustomerID]|OrderID|OrderDate|Prodotto|Quantità|  
|--------------------|-------------|---------------|-------------|--------------|  
|1|256|07/01/2010|Compact Digital|11|  
|1|255|03/01/2010|SLR Camera|15|  
|2|254|03/01/2010|Budget Movie-Maker|27|  
  
 Se si importano tali tabelle dallo stesso database, l'Importazione guidata tabella consente di rilevare le relazioni tra le tabelle in base alle colonne tra [parentesi] e di riprodurre tali relazioni in Progettazione modelli. Per altre informazioni, vedere [Inferenza e rilevamento automatici delle relazioni](#detection) in questo argomento. Se si importano tabelle da più origini, è possibile creare manualmente relazioni come descritto in [Creare una relazione tra due tabelle &#40;SSAS tabulare&#41;](create-a-relationship-between-two-tables-ssas-tabular.md).  
  
### <a name="columns-and-keys"></a>Colonne e chiavi  
 Le relazioni sono basate su colonne in ogni tabella contenente gli stessi dati. Ad esempio, le tabelle Customers e Orders possono essere correlate tra loro poiché contengono entrambe una colonna che memorizza un ID cliente. Nell'esempio, i nomi della colonna sono gli stessi ma questo non è un requisito. Uno potrebbe essere CustomerID e l'altro CustomerNumber, è sufficiente che tutte le righe nella tabella Orders contengano un ID memorizzato anche nella tabella Customers.  
  
 In un database relazionale esistono molti tipi di *chiavi*, in genere semplici colonne con proprietà speciali. I quattro tipi seguenti di chiavi possono essere utilizzati nei database relazionali:  
  
-   *Chiave primaria*: identifica in modo univoco una riga in una tabella, ad esempio CustomerID nella tabella Customers.  
  
-   *Chiave alternativa* (o *chiave candidata*): una colonna diversa dalla chiave primaria univoca. Ad esempio, una tabella Employees potrebbe memorizzare un ID dipendente e un numero di previdenza sociale, entrambi univoci.  
  
-   *Chiave esterna*: una colonna che fa riferimento a una colonna univoca in un'altra tabella, ad esempio CustomerID nella tabella Orders, che fa riferimento a CustomerID nella tabella Customers.  
  
-   *Chiave composta*: chiave composta da più di una colonna. Le chiavi composte non sono supportate nei modelli tabulari. Per altre informazioni, vedere "Chiavi composte e colonne di ricerca" in questo argomento.  
  
 Nei modelli tabulari la chiave primaria o la chiave alternativa viene definita *colonna di ricerca correlata*o semplicemente *colonna di ricerca*. Se una tabella dispone sia di una chiave primaria che di una alternativa, è possibile usare una delle due come colonna di ricerca. La chiave esterna viene definita *colonna di origine* o semplicemente *colonna*. Nell'esempio, viene definita una relazione tra CustomerID nella tabella Orders (la colonna) e CustomerID (la colonna di ricerca) nella tabella Customers. Se vengono importati dati da un database relazionale, per impostazione predefinita, Progettazione modelli sceglie la chiave esterna da una tabella e la chiave primaria corrispondente dall'altra. È tuttavia possibile usare qualsiasi colonna che disponga di valori univoci per la colonna di ricerca.  
  
### <a name="types-of-relationships"></a>Tipi di relazioni  
 La relazione tra Customers e Orders rappresenta una *relazione uno-a-molti*. Ogni cliente può disporre di più ordini ma un ordine non può disporre di più clienti. Gli altri tipi di relazioni sono *uno-a-uno* e *molti-a-molti*. La tabella CustomerDiscounts, che definisce un solo tasso di sconto per ogni cliente, è in una relazione uno-a-uno con la tabella Customers. Un esempio di una relazione molti-a-molti è una relazione diretta tra le tabelle Products e Customers, in cui un cliente può acquistare molti prodotti e lo stesso prodotto può essere acquistato da molti clienti. Progettazione modelli non supporta relazioni molti-a-molti nell'interfaccia utente. Per altre informazioni, vedere "[Relazioni molti-a-molti](#bkmk_many_to_many)" in questo argomento.  
  
 Nella tabella seguente sono riportate le relazioni tra le tre tabelle:  
  
|Relazione|Type|colonna di ricerca|Colonna|  
|------------------|----------|-------------------|------------|  
|Customers-CustomerDiscounts|uno-a-uno|Customers.CustomerID|CustomerDiscounts.CustomerID|  
|Customers-Orders|uno-a-molti|Customers.CustomerID|Orders.CustomerID|  
  
### <a name="relationships-and-performance"></a>Relazioni e prestazioni  
 Dopo aver creato una relazione, Progettazione modelli richiede generalmente il ricalcolo delle formule in cui sono usate le colonne provenienti dalle tabelle della relazione appena creata. L'elaborazione può richiedere del tempo, a seconda della quantità di dati e della complessità delle relazioni.  
  
##  <a name="requirements-for-relationships"></a><a name="requirements"></a>Requisiti per le relazioni  
 Progettazione modelli prevede che vengano rispettati diversi requisiti durante la creazione di relazioni:  
  
### <a name="single-active-relationship-between-tables"></a>Singola relazione attiva tra tabelle  
 Più relazioni possono comportare dipendenze ambigue tra le tabelle. Per creare calcoli accurati, è necessario un unico percorso da una tabella a quella successiva. Di conseguenza, può essere presente una sola relazione attiva tra ogni coppia di tabelle. In AdventureWorks DW 2012, ad esempio, la tabella DimDate contiene una colonna, DateKey, correlata a tre colonne diverse della tabella FactInternetSales: OrderDate, DueDate e ShipDate. Se si tenta di importare queste tabelle, la prima relazione viene creata correttamente, ma per le relazioni successive che riguardano la stessa colonna verrà visualizzato il messaggio di errore seguente:  
  
 \*Relazione: tabella [colonna 1]-> tabella [colonna 2]-stato: errore-motivo: Impossibile creare una relazione tra le tabelle \<tabella 1> e \<tabella 2>. Tra due tabelle può esistere solo una relazione diretta o indiretta.  
  
 Se sono presenti due tabelle unite da più relazioni, sarà necessario importare più copie della tabella contenente la colonna di ricerca e creare una relazione tra ogni coppia di tabelle.  
  
 Possono esistere molte relazioni inattive tra tabelle. Il percorso da utilizzare tra le tabelle viene specificato dallo strumento client di creazione report in fase di query.  
  
### <a name="one-relationship-for-each-source-column"></a>Una relazione per ogni colonna di origine  
 Una colonna di origine non può partecipare a più relazioni. Se una colonna è già stata utilizzata come colonna di origine in una relazione ma si desidera utilizzarla per connetterla a un'altra colonna di ricerca correlata in una tabella diversa, è possibile creare una copia della colonna e utilizzare tale colonna per la nuova relazione.  
  
 Creare una copia di una colonna che dispone esattamente degli stessi valori è un'operazione semplice, eseguibile tramite una formula DAX in una colonna calcolata. Per altre informazioni, vedere [Creare una colonna calcolata &#40;SSAS tabulare&#41;](ssas-calculated-columns-create-a-calculated-column.md).  
  
### <a name="unique-identifier-for-each-table"></a>Identificatore univoco per ogni tabella  
 In ogni tabella deve essere presente una colonna singola che ne identifichi in maniera univoca ogni riga. La colonna correlata viene spesso definita chiave primaria.  
  
### <a name="unique-lookup-columns"></a>Colonne di ricerca univoche  
 I valori dei dati nella colonna di ricerca devono essere univoci. In altri termini, nella colonna non possono essere contenuti valori duplicati. Nei modelli tabulari le stringhe Null e vuote sono equivalenti a un valore vuoto, ovvero un valore dei dati distinto. Ciò vuole dire che non è possibile avere più valori Null nella colonna di ricerca.  
  
### <a name="compatible-data-types"></a>Tipi di dati compatibili  
 I tipi di dati nella colonna di origine e nella colonna di ricerca devono essere compatibili. Per altre informazioni sui tipi di dati, vedere [Tipi di dati supportati &#40;SSAS tabulare&#41;](data-types-supported-ssas-tabular.md).  
  
### <a name="composite-keys-and-lookup-columns"></a>Chiavi composte e colonne di ricerca  
 Non è possibile utilizzare chiavi composte in un modello tabulare. È necessario che vi sia sempre esattamente una colonna che consente di identificare in modo univoco ogni riga nella tabella. Se si tenta di importare tabelle con una relazione esistente basata su una chiave composta, la relazione viene ignorata dall'Importazione guidata tabella, in quanto non può essere creata nel modello tabulare.  
  
 Se si desidera creare una relazione tra due tabelle in Progettazione modelli e sono presenti più colonne che consentono di definire le chiavi primarie ed esterne, è necessario combinare i valori per creare una singola colonna chiave prima di creare la relazione. Tale operazione può essere effettuata prima di importare i dati oppure in Progettazione modelli creando una colonna calcolata.  
  
###  <a name="many-to-many-relationships"></a><a name="bkmk_many_to_many"></a>Relazioni molti-a-molti  
 I modelli tabulari non supportano relazioni molti-a-molti e non è possibile aggiungere semplicemente *tabelle di collegamento* in Progettazione modelli. È tuttavia possibile utilizzare funzioni DAX per modellare relazioni molti-a-molti.  
  
### <a name="self-joins-and-loops"></a>Self-join e cicli  
 I self-join non sono consentiti nelle tabelle del modello tabulare. Un self-join è una relazione ricorsiva tra una tabella e se stessa. I self-join vengono spesso utilizzati per definire gerarchie padre-figlio. Ad esempio, è possibile unire una tabella Employees a se stessa in modo da creare una gerarchia che mostra la catena di gestione di un'azienda.  
  
 Progettazione modelli non consente la creazione di cicli tra relazioni in un modello. In altre parole, il set di relazioni seguente non è consentito.  
  
 Da Table 1, column a   a   Table 2, column f  
  
 Da Table 2, column f   a   Table 3, column n  
  
 Da Table 3, column n   a   Table 1, column a  
  
 Se si tenta di creare una relazione che comporterebbe la creazione di un ciclo, viene generato un errore.  
  
##  <a name="inference-of-relationships"></a><a name="detection"></a>Inferenza delle relazioni  
 In alcuni casi, le relazioni tra le tabelle vengono concatenate automaticamente. Se ad esempio si crea una relazione tra i primi due set di tabelle indicati di seguito, viene dedotta l'esistenza di una relazione tra le altre due tabelle e viene stabilita automaticamente una relazione.  
  
 Products e Category -- creata manualmente  
  
 Category e SubCategory -- creata manualmente  
  
 Products e SubCategory -- relazione dedotta  
  
 Affinché relazioni vengano concatenate automaticamente, le relazioni devono andare in una direzione, come riportato in precedenza. Se le relazioni iniziali erano tra, ad esempio, Sales e Products e Sales e Customers, la relazione non viene dedotta. Ciò avviene perché la relazione tra Products e Customers è una relazione molti-a-molti.  
  
##  <a name="detection-of-relationships-when-importing-data"></a><a name="bkmk_detection"></a>Rilevamento di relazioni durante l'importazione di dati  
 Quando si importano dati da una tabella dell'origine dati relazionale, l'Importazione guidata tabella rileva le relazioni esistenti in tali tabelle di origine basate sui dati dello schema di origine. Se vengono importate tabelle correlate, tali relazioni verranno duplicate nel modello.  
  
##  <a name="manually-create-relationships"></a><a name="bkmk_manually_create"></a>Creazione manuale di relazioni  
 Sebbene la maggior parte delle relazioni tra tabelle in una singola origine dati relazionale vengano rilevate automaticamente e create nel modello tabulare, vi sono casi in cui le relazioni tra le tabelle del modello devono essere create manualmente.  
  
 Se il modello contiene dati da più origini, è probabile che le relazioni debbano essere create manualmente. È ad esempio possibile importare le tabelle Customers, CustomerDiscounts e Orders da un'origine dati relazionale. Le relazioni esistenti tra queste tabelle all'origine vengono create automaticamente nel modello. È quindi possibile aggiungere un'altra tabella da un'origine diversa, ad esempio, importare dati dell'area da una tabella Geography in una cartella di lavoro di Microsoft Excel. È quindi possibile creare manualmente una relazione tra una colonna nella tabella Customers e una colonna nella tabella Geography.  
  
 Per creare manualmente relazioni in un modello tabulare, è possibile utilizzare Progettazione modelli nella Vista diagramma o la finestra di dialogo Gestisci relazioni. Nella Vista diagramma sono visualizzate le tabelle, con le relative relazioni, in formato grafico. È possibile fare clic su una colonna in una tabella e trascinare il cursore in un'altra tabella per creare facilmente una relazione, nell'ordine corretto, tra le tabelle. Nella finestra di dialogo Gestisci relazioni vengono visualizzate relazioni tra tabelle in un formato tabella semplice. Per istruzioni sulla creazione manuale di relazioni, vedere [Creare una relazione tra due tabelle &#40;SSAS tabulare&#41;](create-a-relationship-between-two-tables-ssas-tabular.md).  
  
##  <a name="duplicate-values-and-other-errors"></a><a name="bkmk_dupl_errors"></a>Valori duplicati e altri errori  
 Se si sceglie una colonna che non può essere utilizzata nella relazione, accanto alla colonna viene visualizzata una X rossa. È possibile passare il cursore sull'icona di errore per visualizzare un messaggio in cui sono contenute ulteriori informazioni sul problema. Di seguito sono riportati alcuni dei problemi che possono impedire la creazione di una relazione tra le colonne selezionate:  
  
|Problema o messaggio|Risoluzione|  
|------------------------|----------------|  
|Impossibile creare la relazione perché in entrambe le colonne selezionate sono contenuti valori duplicati.|Per creare una relazione valida, in almeno una colonna della coppia selezionata devono essere contenuti solo valori univoci.<br /><br /> È possibile modificare le colonne per rimuovere i duplicati o invertire l'ordine delle colonne in modo che la colonna in cui sono contenuti i valori univoci venga usata come **Colonna di ricerca correlata**.|  
|Nella colonna è presente un valore Null o vuoto.|Non è possibile creare un join tra le colonne di dati in base a un valore Null. In entrambe le colonne utilizzate in una relazione deve essere presente un valore per ogni riga.|  
  
##  <a name="related-tasks"></a><a name="bkmk_related_tasks"></a> Attività correlate  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Creare una relazione tra due tabelle &#40;SSAS tabulare&#41;](create-a-relationship-between-two-tables-ssas-tabular.md)|Viene descritto come creare manualmente una relazione tra due tabelle.|  
|[Eliminare relazioni &#40;SSAS tabulare&#41;](relationships-ssas-tabular.md)|Viene descritto come eliminare una relazione e le ramificazioni dovute all'eliminazione di relazioni.|  
  
## <a name="see-also"></a>Vedi anche  
 [Tabelle e colonne &#40;SSAS tabulare&#41;](tables-and-columns-ssas-tabular.md)   
 [Importare dati &#40;SSAS tabulare&#41;](../import-data-ssas-tabular.md)  
  
  
