---
title: Creare un cubo da un modello senza utilizzare una vista origine dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5c8c09b1-140c-48db-9b9f-d18a051d7dbd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0125550f8ec4a3fa290ea29df3d33cc3bebe3c7e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62700316"
---
# <a name="create-a-cube-from-a-template-without-using-a-data-source-view"></a>Creare un cubo da un modello senza utilizzare una vista origine dati
  Selezionare **Build the cube without using a data source** (Crea il cubo senza usare un'origine dati) nella prima pagina di Creazione guidata cubo per creare un cubo senza usare una vista origine dati. Successivamente è possibile usare Generazione guidata schema per generare lo schema relazionale per la vista origine dati in base alla struttura del cubo e possibilmente ad altri oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni sulla generazione di uno schema, vedere [Generazione guidata schema &#40;Analysis Services&#41;](schema-generation-wizard-analysis-services.md).  
  
## <a name="selecting-the-build-method"></a>Selezione del metodo di compilazione  
 Nella pagina **Selezione metodo di creazione** della procedura guidata fare clic su **Build the cube without using a data source**(Crea il cubo senza usare un'origine dati). Per creare il cubo usando un modello di cubo esistente, selezionare la casella di controllo **Use a cube template** (Usa un modello di cubo). . Se non si seleziona l'utilizzo di un modello, è necessario impostare le opzioni manualmente.  
  
 Nei modelli di cubo sono inclusi misure, gruppi di misure, dimensioni, gerarchie e attributi predefiniti. Se si seleziona un modello, nella procedura guidata vengono utilizzate le definizioni di oggetti nei modelli come base per l'impostazione delle opzioni nelle pagine seguenti. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene installato con diversi modelli di cubi standard. L'amministratore del server può aggiungere inoltre modelli di cubo o di dimensioni progettati espressamente per i dati dell'organizzazione.  
  
## <a name="selecting-dimensions"></a>Selezione delle dimensioni  
 Utilizzare la pagina per **selezionare le dimensioni** della procedura guidata per aggiungere dimensioni esistenti al cubo. Questa pagina viene visualizzata solo se esistono già dimensioni condivise senza un'origine dati nel progetto o nel database. In essa non sono elencate dimensioni che dispongono di un'origine dati.  
  
 Per aggiungere dimensioni esistenti, selezionare una o più dimensioni nell'elenco **Dimensioni condivise** e fare clic sul pulsante con la freccia a destra (**>**) per spostarle nell'elenco **Dimensioni cubo** . Fare clic sul pulsante con la doppia freccia (**>>**) per spostare tutte le dimensioni nell'elenco.  
  
## <a name="defining-new-measures"></a>Definizione di nuove misure  
 Usare la pagina **Definizione nuove misure** della procedura guidata per specificare le misure e i gruppi di misure nel nuovo cubo. I gruppi di misure che vengono specificati in questa pagina corrisponderanno alle tabelle dei fatti nello schema generato, mentre le misure corrisponderanno alle colonne non chiave numeriche nelle tabelle.  
  
 Se si uso un modello per creare il cubo, le misure nel modello vengono elencate in formato griglia in **Selezionare le misure dal modello**. Inizialmente sono selezionate tutte le caselle di controllo accanto a ogni misura dell'elenco. È possibile deselezionare le caselle relative a qualsiasi misura che non si desidera includere nel cubo. Per aggiungere o rimuovere tutte le misure nell'elenco, selezionare o deselezionare la casella di controllo nella barra del titolo della griglia.  
  
 È possibile aggiungere misure al cubo nell'elenco in **Aggiungi nuove misure**. Per aggiungere una nuova misura, fare clic sulla prima cella vuota nella colonna **Nome misura** in cui è visualizzata l'indicazione **Aggiungi nuova misura**. Specificare un nome di misura, un gruppo di misure, un tipo di dati e un'aggregazione per ogni nuova misura. Per eliminare una misura dall'elenco **Aggiungi nuove misure** , fare clic sull'icona di eliminazione (**X**). Se non si usa un modello, **Aggiungi nuove misure** è l'unico elenco presente in questa pagina della procedura guidata.  
  
 Sia nella griglia **Selezionare le misure dal modello** sia nella griglia **Aggiungi nuove misure** vengono visualizzati i valori delle colonne descritte nella tabella seguente. È possibile fare clic su un valore in entrambi gli elenchi per modificarlo.  
  
|colonna|Descrizione|  
|------------|-----------------|  
|**Nome misura**|Un valore in questa colonna consente di definire il nome di una misura nel cubo. Fare clic su un valore in questa colonna per digitare un nome. Fare clic su **Aggiungi nuova misura** in questa colonna per creare una nuova misura. Questa colonna consente di impostare la proprietà `Name` nell'oggetto misura.|  
|**Gruppo di misure**|Nome del gruppo di misure contenente la misura. Fare clic su questo valore per scegliere o digitare un nome. Se si eliminano tutte le misure che appartengono a un particolare gruppo, viene rimosso anche quest'ultimo. Questa colonna consente di impostare la proprietà `Name` per l'oggetto gruppo di misure.|  
|**Tipo di dati**|Tipo di dati per la misura. Fare clic su questo valore per modificare il tipo di dati. Il valore predefinito quando si crea una misura è `Single`. Questa colonna consente di impostare la proprietà `DataType` nell'oggetto misura.|  
|**Aggregazione**|Aggregazione standard per la misura. Fare clic su questa cella per specificare una delle aggregazioni standard per la misura (o **Nessuna**). Il valore predefinito quando si crea una misura è `Sum`. Questa colonna consente di impostare la proprietà `AggregationFunction` nell'oggetto misura.|  
  
## <a name="defining-new-dimensions"></a>Definizione di nuove dimensioni  
 Usare la pagina **Definizione nuove dimensioni** della procedura guidata per specificare le dimensioni nel nuovo cubo.  
  
 Se si usa un modello per creare il cubo, nella griglia in **Selezionare le dimensioni dal modello** vengono visualizzate le dimensioni nel modello. È possibile deselezionare la casella di controllo accanto a una qualsiasi dimensione per rimuoverla dal cubo. Deselezionare la casella di controllo nella barra del titolo della griglia per rimuovere tutte le dimensioni elencate. Se non si utilizza un modello, nella griglia viene elencata solo la dimensione temporale.  
  
 È possibile aggiungere dimensioni al cubo nella griglia in **Aggiungi nuove dimensioni**. Per aggiungere una dimensione, fare clic nella cella le `Name` colonna che contiene il testo **Aggiungi nuova dimensione**e quindi digitare un nome per la dimensione. Per rimuovere una riga dall'elenco, fare clic sull'icona di eliminazione (**X**).  
  
 Sia nella griglia **Selezionare le dimensioni dal modello** sia nella griglia **Aggiungi nuove dimensioni** vengono visualizzati i valori delle colonne descritte nella tabella seguente. È possibile fare clic su un valore in entrambi gli elenchi per modificarlo.  
  
|colonna|Descrizione|  
|------------|-----------------|  
|**Tipo**|Viene visualizzato il tipo di dimensione per una dimensione del modello. Fare clic su questa cella per modificare il tipo di dimensione per una dimensione. Questa colonna consente di impostare la proprietà **Tipo** per l'oggetto dimensione.|  
|`Name`|Viene visualizzato il nome della dimensione. Fare clic su questa cella per digitare un nome diverso. Questo valore imposta la `Name` proprietà per l'oggetto dimensione.|  
|**Dimensione a modifica lenta**|Viene specificato che si tratta di una dimensione a modifica lenta. Se si seleziona questa casella di controllo, alla dimensione vengono aggiunti gli attributi relativi alla data di inizio, alla data di fine, all'ID originale e allo stato della dimensione a modifica lenta. L'opzione**Dimensione a modifica lenta** è selezionata per impostazione predefinita se si usa un modello per creare il cubo e la procedura guidata rileva questi quattro tipi di attributo in una dimensione del modello.|  
|**Attributi**|Vengono visualizzati gli attributi che devono essere creati per la dimensione. Ogni nome di attributo nell'elenco è preceduto dal nome della dimensione. Questo elenco è di sola lettura. È possibile modificare gli attributi tramite Progettazione dimensioni dopo il completamento della procedura guidata.|  
  
## <a name="defining-time-periods"></a>Definizione dei periodi di tempo  
 Usare la pagina **Definizione periodi di tempo** della procedura guidata per specificare l'intervallo di date da includere nella dimensione. È possibile scegliere, ad esempio, un intervallo che inizia dal primo gennaio del primo anno a cui si riferiscono i dati e che si estende fino agli anni successivi alla transazione più recente. Le transazioni che non rientrano in questo intervallo non verranno visualizzate oppure verranno visualizzate come membri sconosciuti nella dimensione in base all'impostazione della proprietà `UnknownMemberVisible` della dimensione. La proprietà `UnknownMemberName` consente di specificare la didascalia per il membro sconosciuto. È inoltre possibile modificare il primo giorno della settimana utilizzato nei dati. Il giorno predefinito è domenica.  
  
> [!NOTE]  
>  La pagina **Definizione periodi di tempo** viene visualizzata solo se si include una dimensione temporale nel cubo nella pagina **Definizione nuove dimensioni** della procedura guidata.  
  
 Selezionare i periodi di tempo, vale a dire**Anno**, **Semestre**, **Trimestre**, **Quadrimestre**, **Mese**, **Decade**, **Settimana**e **Data**, da includere nello schema. È necessario selezionare il periodo di tempo Data il cui attributo è quello chiave della dimensione e senza il quale la dimensione non può funzionare. Inoltre, è possibile modificare la lingua utilizzata per identificare i membri della dimensione.  
  
 I periodi di tempo selezionati consentono di creare gli attributi temporali corrispondenti nella nuova dimensione temporale. Inoltre, la procedura guidata consente di aggiungere i relativi attributi che non vengono visualizzati nell'elenco. Ad esempio, se si selezionano gli intervalli di tempo **Anno** e **Semestre** , la procedura guidata crea gli attributi Giorno dell'anno, Giorno del semestre e Semestri dell'anno, oltre agli attributi Anno e Semestre.  
  
 Al termine della creazione del cubo, è possibile utilizzare Progettazione dimensioni per aggiungere o rimuovere gli attributi temporali. Dal momento che Data è l'attributo chiave per la dimensione, non è possibile rimuoverlo. Per nascondere l'attributo Data agli utenti, è possibile impostare la proprietà `AttributeHierarchyVisible` su `False`.  
  
 Tutti i periodi di tempo disponibili sono visualizzati nel riquadro Periodi di tempo di Progettazione dimensioni. Questo riquadro sostituisce quello denominato **Vista origine dati** per le dimensioni basate sulle tabelle delle dimensioni. L'intervallo di date per una dimensione può essere modificato cambiando l'impostazione della proprietà **Origine** (associazione temporale) per la dimensione. Poiché si tratta di una modifica strutturale, è necessario rielaborare la dimensione e tutti i cubi in cui viene utilizzata prima di visualizzare i dati.  
  
## <a name="specifying-additional-calendars"></a>Specifica di calendari aggiuntivi  
 Nella pagina **Impostazione calendari aggiuntivi** della procedura guidata selezionare i calendari su cui basare le gerarchie nella dimensione. È possibile scegliere i calendari indicati di seguito.  
  
|Calendario|Descrizione|  
|--------------|-----------------|  
|Calendario fiscale|Calendario fiscale di dodici mesi. Se si seleziona questo calendario, specificare il giorno e il mese di inizio dell'anno fiscale in uso nell'organizzazione.|  
|Calendario report (o marketing)|Calendario di report di dodici mesi in cui sono inclusi due mesi di quattro settimane e un mese di cinque settimane in un modello periodico di tre mesi (trimestre). Se si seleziona questo calendario, specificare il giorno e mese e il modello di tre mesi di 4-4 e 5, 4-5-4 o 5-4-4 settimane, dove ogni cifra rappresenta il numero di settimane al mese.|  
|Calendario produzione|Calendario in cui vengono utilizzati 13 periodi di quattro settimane, divisi in tre trimestri di quattro periodi e un trimestre di cinque periodi. Se si seleziona questo calendario, specificare la settimana di inizio, compresa tra 1 e 4, il mese per l'anno di produzione, nonché il trimestre con periodi aggiuntivi.|  
|Calendario ISO 8601|Calendario standard ISO (International Organization for Standardization) per il formato della data e dell'ora (8601). Calendario costituito da un numero intero di settimane di sette giorni. Per evitare di dividere una settimana, il calendario inizia un nuovo anno pochi giorni prima o dopo il primo gennaio.|  
  
 Il calendario e le impostazioni selezionate consentono di determinare gli attributi creati nella dimensione. Se, ad esempio, nella pagina **Definizione periodi di tempo** della procedura guidata si selezionano i periodi di tempo **Anno** e **Trimestre** , nonché **Calendario fiscale** , vengono creati i relativi attributi FiscalYear, FiscalQuarter e FiscalQuarterOfYear.  
  
 Inoltre, la procedura guidata consente di creare gerarchie specifiche del calendario composte da attributi creati per il calendario. Per ogni calendario, ogni livello di ogni gerarchia è sottoposto al rollup nel livello superiore. Ad esempio, nel calendario standard di 12 mesi la procedura guidata crea una gerarchia con anni e settimane o anni e mesi. Le settimane non sono però ripartite in modo uniforme tra i mesi di un calendario standard, pertanto non esiste una gerarchia con anni, mesi e settimane. Viceversa, in un calendario di report o produzione le settimane sono suddivise in modo uniforme tra i mesi, pertanto viene eseguito il rollup delle settimane nei mesi.  
  
## <a name="defining-dimension-usage"></a>Definizione dell'utilizzo delle dimensioni  
 Usare la pagina **Definizione utilizzo delle dimensioni** della procedura guidata per specificare quali misure del cubo vengono aggregate da ogni dimensione nella procedura guidata. Le dimensioni e i gruppi di misure nella griglia **Utilizzo dimensioni** di questa pagina sono elencate rispettivamente come righe e colonne. Selezionare la casella di controllo per qualsiasi combinazione di dimensione e gruppo di misure in cui, mediante la dimensione, vengono aggregate le misure di tale gruppo di misure.  
  
## <a name="completing-the-cube-wizard"></a>Completamento della Creazione guidata cubo  
 Nella pagina **Completamento procedura guidata** verificare la struttura del nuovo cubo e nella casella **Nome cubo** digitare un nome per il cubo. Facoltativamente, selezionare la casella di controllo **Genera schema adesso** per avviare Generazione guidata schema. Nella maggior parte dei casi non è necessario selezionare questa casella di controllo quando si pianifica la creazione di oggetti aggiuntivi. Inoltre, è possibile utilizzare Progettazione cubi per generare lo schema in un secondo momento.  
  
  
