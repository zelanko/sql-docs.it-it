---
title: Concetti di CSDLBI | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 2fbdf621-a94d-4a55-a088-3d56d65016ac
author: minewiskan
ms.author: owend
ms.openlocfilehash: 16c6597171eef10da67ad497e4303b3716298e6a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940128"
---
# <a name="csdlbi-concepts"></a>Concetti di CSDLBI
  Il linguaggio CSDL (Conceptual Schema Definition Language) con annotazioni Business Intelligence (CSDLBI) è basato su Entity Data Framework, ovvero un'astrazione per la rappresentazione di dati in modo da rendere possibile l'accesso, l'esecuzione di query o l'esportazione di set di dati diversi a livello di programmazione. CSDLBI viene utilizzato per rappresentare i modelli di dati creati utilizzando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] perché supporta le applicazioni e la creazione di rapporti guidata dai dati e avanzata.  
  
 In questa sezione viene illustrato come la rappresentazione CSDLBI esegue il mapping ai modelli di dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (tabulari e multidimensionali), insieme a esempi per ogni tipo di modello.  
  
 Gli esempi utilizzati per illustrare questi provengono dal database di esempio AdventureWorks, disponibile su Codeplex. Per ulteriori informazioni sugli esempi, vedere [esempi di Adventure Works per SQL Server](https://go.microsoft.com/fwlink/?linkID=220093).  
  
## <a name="structure-of-a-tabular-model-in-csdlbi"></a>Struttura di un modello tabulare in CSDLBI  
 Un documento CSDLBI che descrive un modello di report e i relativi dati inizia con l'istruzione xsd, seguito dalla definizione di un modello.  
  
 Il modello è uno spazio dei nomi che contiene le seguenti entità, associazioni e proprietà principali:  
  
-   In `EntityContainer` sono elencate le tabelle del modello.  
  
-   Ogni tabella viene elencata con `EntityContainer` come `EntitySet`.  
  
-   Ogni relazione tra due tabelle viene descritta come `AssociationSet` che definisce gli endpoint e i ruoli della relazione.  
  
-   L'elemento `EntityType` viene esteso per BISM per fornire dettagli aggiuntivi sulle tabelle e sulle relative colonne, incluse le proprietà utilizzate a scopo di ordinamento e visualizzazione.  
  
-   L'elemento `Measure` definisce i calcoli che è possibile utilizzare nel modello. Una misura può essere trasformata in un indicatore KPI aggiungendo un set di attributi di visualizzazione speciali tramite il nuovo elemento `KPI`.  
  
-   Non sono disponibili rappresentazioni di prospettive distinte. Le colonne e le tabelle non incluse in una prospettiva sono presenti in CSDL, ma contrassegnate con l'attributo `Hidden`.  
  
### <a name="entities-entitysets-and-entitytypes"></a>Entità, EntitySet ed EntityType  
 La nozione di un'entità in Entity Data Framework viene estesa per rappresentare colonne e tabelle del modello di dati. Nell'estratto seguente è riportato l'elenco di elementi `EntitySet` in un modello semplice che contiene solo tre tabelle.  
  
```  
<EntityContainer Name="SimpleModel">  
<EntitySet Name="DimCustomer"EntityType="SimpleModel.DimCustomer">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimDate" EntityType="SimpleModel.DimDate">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimGeography" EntityType="SimpleModel.DimGeography">  
     <bi:EntitySet />  
   </EntitySet> />  
  
```  
  
 `EntitySet` non contiene informazioni su colonne o dati inclusi nella tabella. La descrizione dettagliata delle colonne e delle relative proprietà viene fornita nell'elemento EntityType.  
  
 L'elemento `EntitySet` per ogni entità (tabella) include una raccolta di proprietà che definiscono la colonna chiave, il tipo di dati e la lunghezza della colonna, l'utilizzo dei valori Null, il tipo di ordinamento e così via. Ad esempio, nell'estratto di CSDL seguente vengono descritte tre colonne nella tabella Customer. La prima colonna è una colonna nascosta speciale utilizzata internamente dal modello.  
  
```  
<EntityType Name="Customer">  
  <Key>  
     <PropertyRef Name="RowNumber" />  
  </Key>  
    <Property Name="RowNumber" Type="Int64" Nullable="false">  
     <bi:Property Hidden="true" Contents="RowNumber"  
       Stability="RowNumber" />  
    </Property>  
    <Property Name="CustomerKey" Type="Int64" Nullable="false">  
      <bi:Property />  
    </Property>  
     <Property Name="FirstName" Type="String" MaxLength="Max" FixedLength="false">  
       <bi:Property />  
      </Property>  
  
```  
  
 Per limitare le dimensioni del documento CSDLBI generato, le proprietà visualizzate più di una volta in un'entità vengono specificate mediante un riferimento a una proprietà esistente, in modo che sia necessario elencare la proprietà una sola volta per `EntityType`. L'applicazione client può ottenere il valore della proprietà mediante la ricerca dell'elemento `EntityType` corrispondente a `OriginEntityType`.  
  
### <a name="relationships"></a>Relazioni  
 In Entity Data Framework le relazioni sono definite come *associazioni* tra entità.  
  
 Le associazioni dispongono sempre esattamente di due endpoint, ognuno dei quali punta a un campo o una colonna in una tabella. Tra due tabelle sono pertanto possibili più relazioni, se queste ultime dispongono di endpoint diversi. Agli endpoint dell'associazione viene assegnato un nome di ruolo, che indica come viene utilizzata l'associazione nel contesto del modello di dati. Un esempio di un nome di ruolo potrebbe essere **ShipTo**, quando viene applicato a un ID cliente correlato all'ID cliente in una tabella Orders.  
  
 La rappresentazione CSDLBI del modello contiene anche attributi sull'associazione che determinano la modalità di mapping tra le entità in termini di *molteplicità* dell'associazione. La molteplicità indica se l'attributo o la colonna corrispondente all'endpoint di una relazione tra tabelle si trova sul lato uno o sul lato molti di una relazione. Non sono presenti valori distinti per le relazioni uno-a-uno. Le annotazioni CSDLBI supportano una molteplicità pari a 0 (ovvero l'entità non è associata ad alcun elemento) oppure 0..1, per indicare una relazione uno-a-uno o uno-a-molti.  
  
 Nell'esempio seguente viene rappresentato l'output di CSDLBI per una relazione tra le tabelle Date e ProductInventory di cui è stato creato un join alla colonna DateAlternateKey. Si noti che, per impostazione predefinita, il nome di `AssociationSet` è il nome completo delle colonne interessate dalla relazione. È tuttavia possibile modificare questo comportamento quando si progetta il modello, in modo da utilizzare un formato di denominazione diverso.  
  
```  
<AssociationSet Name="ProductInventory_Date_DateKey" Association="Model.ProductInventory_Date_DateKey">  
              <End EntitySet="ProductInventory" />  
              <End EntitySet="Date" />  
              <bi:AssociationSet />  
            </AssociationSet>  
  
```  
  
### <a name="visualization-and-navigation-properties"></a>Proprietà di visualizzazione e navigazione  
 Una parte importante delle annotazioni CSDLBI sono le proprietà per la definizione della presentazione nel livello del report e per la navigazione all'interno delle relazioni tra entità. In genere, quando si crea un modello di dati non si considera importante controllare la modalità di ordinamento o raggruppamento dei dati o quale potrebbe essere il valore predefinito, supponendo che l'ordinamento e gli altri dettagli di presentazione verranno specificati dall'applicazione client. I modelli tabulari di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono tuttavia progettati per l'integrazione con il client di creazione report [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] e includono proprietà e attributi che supportano la presentazione di entità dal modello di dati nell'area di progettazione del report.  
  
 Nelle estensioni per la visualizzazione sono inclusi attributi che consentono di specificare l'aggregazione predefinita da utilizzare con i dati numerici, di indicare che un campo di testo punta all'URL di un'immagine o di specificare il campo utilizzato per l'ordinamento del campo corrente.  
  
### <a name="name-properties-and-naming-conventions"></a>Proprietà dei nomi e convenzioni di denominazione  
 Lo schema CSDLBI indica che ogni entità dispone di un nome univoco e un identificatore che può essere utilizzato come una chiave. Alcune entità possono inoltre disporre di didascalie utilizzate a fini della visualizzazione e di nomi contestuali che vengono modificati a seconda della posizione in cui viene utilizzata l'entità.  
  
 L'elemento `Documentation` offre ai progettisti di report la possibilità di fornire una descrizione dell'entità, per consentire agli utenti aziendali di comprendere il significato dei dati. Alcune entità supportano inoltre uno o più attributi `Annotation`, che forniscono metadati aggiuntivi utilizzabili dall'applicazione o dai client.  
  
 Quando si genera un modello per gli strumenti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], i nomi creati per gli oggetti seguono le convenzioni di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per la denominazione degli oggetti e l'univocità dei nomi. Poiché tuttavia CSDLBI si basa su Entity Data Framework (EDF), in cui è necessario che i nomi rispettino le convenzioni per gli identificatori C#, quando il server crea l'output CSDLBI per un modello, ottiene i nomi utilizzati all'interno dello schema di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e crea automaticamente nuovi nomi di oggetti conformi ai requisiti di EDF. Nella tabella seguente vengono descritte le operazioni tramite le quali vengono generati i nuovi nomi.  
  
|Regola|Azione|  
|----------|------------|  
|Nessun carattere non consentito|I caratteri non consentiti vengono sostituiti da caratteri di sottolineatura.|  
|I nomi devono essere univoci|Se due stringhe sono uguali, una viene resa univoca aggiungendovi un carattere di sottolineatura più un numero|  
  
> [!WARNING]  
>  Sono presenti traduzioni sia per didascalie che per qualificatori e, per un determinato linguaggio, potrebbe essere presenti le une o gli altri. Ciò significa che nei casi in cui siano concatenati un qualificatore e un nome o un qualificatore e una didascalia, è possibile che le stringhe siano in due linguaggi diversi.  
  
## <a name="additions-to-support-multidimensional-models"></a>Aggiunte per supportare modelli multidimensionali  
 La versione 1.0 delle annotazioni CSDLBI supporta solo i modelli tabulari. Nella versione 1.1, è stato aggiunto il supporto per i modelli multidimensionali (cubi OLAP) creati utilizzando gli strumenti di sviluppo tradizionali di Business Intelligence. Pertanto, è ora possibile generare una richiesta XML a un modello multidimensionale e ricevere una definizione CSDLBI del modello da utilizzare nella creazione di rapporti.  
  
 **Cubi:** Un SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database tabulare può contenere una sola modalità. Ciascun database multidimensionale, invece, può contenere più cubi, ogni database associato a un cubo predefinito. Pertanto quando si invia una richiesta XML a un server multidimensionale, è necessario specificare il cubo; in caso contrario, sarà restituito l'XML per il cubo predefinito.  
  
 La rappresentazione di un cubo è molto simile a quella di un database modello tabulare. Il nome del cubo e il cubo corrispondono all'identificatore del database e al nome del database tabulare.  
  
 **Dimensioni:** Una dimensione viene rappresentata in CSDLBI come entità (tabella) con colonne e proprietà. Si noti che anche se non è presente in una prospettiva, una dimensione inclusa nel modello verrà rappresentata nell'output CSDL, contrassegnata come `Hidden`.  
  
 **Prospettive:** Un client può richiedere CSDL per le singole prospettive. Per ulteriori informazioni, vedere [DISCOVER_CSDL_METADATA set di righe](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset).  
  
 **Gerarchie:** Le gerarchie sono supportate e rappresentate in CSDLBI come set di livelli.  
  
 **Membri:** È stato aggiunto il supporto per il membro predefinito e i valori predefiniti vengono aggiunti automaticamente all'output CSDLBI.  
  
 **Membri calcolati:** I modelli multidimensionali supportano i membri calcolati per l'elemento figlio di **All** con un singolo membro reale.  
  
 **Attributi dimensione:** Nell'output di CSDLBI, gli attributi delle dimensioni sono supportati e automaticamente contrassegnati come non aggregabili.  
  
 **Indicatori KPI:** Gli indicatori KPI sono supportati nella versione 1,1 di CSDLBI, ma la rappresentazione è cambiata. Prima, un indicatore KPI era la proprietà di una misura. Nella versione 1.1, l'elemento KPI può essere aggiunto a una misura  
  
 **Nuove proprietà:** Sono stati aggiunti attributi aggiuntivi per supportare i modelli DirectQuery.  
  
 **Limitazioni:** La sicurezza della cella non è supportata.  
  
## <a name="see-also"></a>Vedere anche  
 [Annotazioni CSDL per Business Intelligence &#40;CSDLBI&#41;](/analysis-services/csdlbi/csdl-annotations-for-business-intelligence-csdlbi)  
  
  
