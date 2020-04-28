---
title: Gerarchie utente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- members [Analysis Services], hierarchies
- dimensions [Analysis Services], hierarchies
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], hierarchies
- parent-child hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
- ragged hierarchies [Analysis Services]
- balanced hierarchies [Analysis Services]
- hierarchies [Analysis Services]
- OLAP objects [Analysis Services], hierarchies
- multilevel hierarchies [Analysis Services]
- unbalanced hierarchies [Analysis Services]
ms.assetid: 9394e9a3-2242-4f0e-85e0-25d499d2d3b6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e65da7af45aa2c5dbb18a560b05a5d943a9e64c1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "72811595"
---
# <a name="user-hierarchies"></a>Gerarchie definite dall'utente
  Le gerarchie definite dall'utente sono gerarchie definite dall'utente degli attributi utilizzati in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per organizzare i membri di una dimensione in strutture gerarchiche e fornire percorsi di navigazione in un cubo. Nella tabella seguente viene ad esempio definita una tabella per una dimensione temporale. La tabella delle dimensioni supporta tre attributi, Year, Quarter e Month.  
  
|Year|Quarter|Month|  
|----------|-------------|-----------|  
|1999|Trimestre 1|Gen|  
|1999|Trimestre 1|Feb|  
|1999|Trimestre 1|Mar|  
|1999|Trimestre 2|Apr|  
|1999|Trimestre 2|Mag|  
|1999|Trimestre 2|Giu|  
|1999|Trimestre 3|Lug|  
|1999|Trimestre 3|Ago|  
|1999|Trimestre 3|Set|  
|1999|Trimestre 4|Oct|  
|1999|Trimestre 4|Nov|  
|1999|Trimestre 4|Dec|  
  
 Gli attributi Year, Quarter e Month vengono utilizzati per creare nella dimensione temporale una gerarchia definita dall'utente denominata Calendar. Nella figura riportata di seguito è illustrata la relazione esistente tra i livelli e i membri della dimensione Calendar, che è una dimensione regolare.  
  
 ![Gerarchia di livelli e membri per una dimensione temporale](../dev-guide/media/as-levelconcepts.gif "Gerarchia di livelli e membri per una dimensione temporale")  
  
> [!NOTE]  
>  Tutte le gerarchie diverse dalla gerarchia a due livelli predefinita dell'attributo vengono denominate gerarchie definite dall'utente. Per ulteriori informazioni sulle gerarchie degli attributi, vedere [attributi e gerarchie](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)di attributi.  
  
## <a name="member-structures"></a>Strutture dei membri  
 Ad eccezione delle gerarchie padre-figlio, le posizioni dei membri di una gerarchia vengono controllate dall'ordinamento degli attributi nella definizione della gerarchia. Ogni attributo nella definizione della gerarchia costituisce un livello nella gerarchia. La posizione di un membro all'interno di un livello viene determinata dall'ordinamento dell'attributo utilizzato per creare il livello. Le strutture dei membri delle gerarchie definite dall'utente possono assumere una delle quattro forme di base, a seconda della relazione esistente tra i membri.  
  
### <a name="balanced-hierarchies"></a>Gerarchie bilanciate  
 In una gerarchia bilanciata tutti i rami scendono fino allo stesso livello di dettaglio e il membro padre logico di ogni membro è situato al livello immediatamente superiore rispetto al membro. La gerarchia Product Categories della dimensione Product nel database di esempio [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è un buon esempio di gerarchia bilanciata. Ogni membro nel livello Product Name ha un membro padre nel livello Subcategory che a sua volta ha un membro padre nel livello Category. Ogni ramo nella gerarchia ha inoltre un membro foglia nel livello Product Name.  
  
### <a name="unbalanced-hierarchies"></a>Gerarchie sbilanciate  
 In una gerarchia sbilanciata i rami della gerarchia scendono fino a livelli di dettaglio diversi. Le gerarchie padre-figlio sono gerarchie sbilanciate. Ad esempio, la dimensione Organization nel database di esempio [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contiene un membro per ogni dipendente. Il direttore generale è il membro superiore della gerarchia, mentre i responsabili di divisione e la segretaria di direzione sono immediatamente subordinati al direttore generale. A differenza della segretaria di direzione, i responsabili di divisione hanno membri subordinati.  
  
 Sebbene per gli utenti finali potrebbe essere impossibile distinguere le gerarchie sbilanciate da quelle incomplete, si utilizzano tecniche e proprietà diverse in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per supportare questi due tipi di gerarchia. Per ulteriori informazioni, vedere [gerarchie incomplete](../multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md)e [attributi nelle gerarchie padre-figlio](../multidimensional-models/parent-child-dimension-attributes.md).  
  
### <a name="ragged-hierarchies"></a>Gerarchie incomplete  
 In una gerarchia incompleta, il membro padre logico di almeno un membro non si trova nel livello immediatamente superiore rispetto al membro. Ne consegue che i rami della gerarchia possono scendere a livelli di dettaglio diversi. Ad esempio, in una dimensione Geography definita con i livelli Continent, CountryRegion e City in questo ordine, il membro Europa viene visualizzato nel livello superiore della gerarchia, il membro France nel livello intermedio e il membro Paris nel livello inferiore, in quanto France è più specifico di Europa e Paris è più specifico di France. A questa gerarchia regolare vengono apportate le modifiche seguenti:  
  
-   Il membro Vatican City viene aggiunto al livello CountryRegion.  
  
-   I membri vengono aggiunti al livello City e associati al membro Vatican City nel livello CountryRegion.  
  
-   Un livello denominato Province viene aggiunto tra i livelli CountryRegion e City.  
  
 Il livello Province viene popolato con i membri associati ad altri membri nel livello CountryRegion e i membri nel livello City vengono associati ai membri corrispondenti nel livello Province. Tuttavia, dato che il membro Vatican City nel livello CountryRegion non ha membri associati nel livello Province, i membri devono essere associati dal livello City direttamente al membro Vatican City nel livello CountryRegion. A causa delle modifiche, la gerarchia della dimensione ora risulta incompleta. Il membro padre della città Vatican City è il paese/regione Vatican City che non si trova nel livello immediatamente superiore al membro Vatican City nel livello City. Per altre informazioni, vedere [Gerarchie incomplete](../multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md).  
  
### <a name="parent-child-hierarchies"></a>Gerarchie padre-figlio  
 Le gerarchie padre-figlio delle dimensioni vengono definite utilizzando un attributo speciale, denominato attributo padre, per determinare il tipo di relazione esistente tra i membri. Un attributo padre descrive una *relazione autoreferenziale*, o *self join*, in una tabella della dimensione principale. Le gerarchie padre-figlio vengono create da un unico attributo padre. A una gerarchia padre-figlio viene assegnato un solo livello, in quanto i livelli presenti nella gerarchia sono derivati dalle relazioni padre-figlio tra i membri associati all'attributo padre. Lo schema della dimensione di una gerarchia padre-figlio dipende da una relazione autoreferenziale presente nella tabella della dimensione principale. Nel diagramma seguente, ad esempio, viene illustrata la tabella principale della dimensione di **dimorgan** nel database di [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esempio.  
  
 ![Join autoreferenziale nella tabella DimOrganization](../dev-guide/media/dimorganization.gif "Join autoreferenziale nella tabella DimOrganization")  
  
 In questa tabella della dimensione, nella colonna **dbo.xdbcdc_databases** è inclusa una relazione di chiave esterna con la colonna chiave primaria **OrganizationKey** . In altri termini, ogni record di questa tabella può essere messo in relazione a un altro record della tabella tramite una relazione padre-figlio. Questo tipo di self join viene in genere utilizzato per rappresentare dati entità dell'organizzazione, ad esempio la struttura di gestione dei dipendenti in un reparto.  
  
 Quando si crea una gerarchia padre-figlio, le colonne rappresentate da entrambi gli attributi devono contenere lo stesso tipo di dati ed essere inserite nella stessa tabella. Per impostazione predefinita tutti i membri per cui la chiave del padre corrisponde alla chiave del membro stesso, a Null, a 0 (zero) o a un valore non presente nella colonna delle chiavi dei membri vengono considerati membri del primo livello, escluso il livello (Totale).  
  
 Il livello di nidificazione di una gerarchia padre-figlio può variare da un ramo all'altro della gerarchia. In altre parole, una gerarchia padre-figlio viene considerata una gerarchia sbilanciata.  
  
 A differenza delle gerarchie definite dall'utente, in cui il numero dei livelli presenti nella gerarchia determina il numero dei livelli visualizzabili dagli utenti finali, le gerarchie padre-figlio vengono definite dall'unico livello della gerarchia dell'attributo e i diversi livelli visualizzati dagli utenti sono prodotti dai valori di questo singolo livello. Il numero di livelli visualizzati dipende dal contenuto delle colonne della tabella della dimensione in cui vengono archiviate le chiavi dei membri e le chiavi dei membri padre. Il numero di livelli può cambiare se vengono modificati i dati nelle tabelle della dimensione. Per ulteriori informazioni, vedere [gerarchia padre-figlio](../multidimensional-models/parent-child-dimension.md)e [attributi nelle gerarchie padre-figlio](../multidimensional-models/parent-child-dimension-attributes.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di gerarchie definite dall'utente](../multidimensional-models/user-defined-hierarchies-create.md)   
 [Proprietà gerarchia utente](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Riferimento alle proprietà degli attributo delle dimensioni](../multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
