---
title: Relazioni tra dimensioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- relationships [Analysis Services]
- member groups [Analysis Services]
- regular dimensions [Analysis Services]
- many-to-many relationships [Analysis Services]
- cubes [Analysis Services], relationships
- reference dimensions
- dimensions [Analysis Services], relationships
- fact dimensions [Analysis Services]
- relationships [Analysis Services], dimensions
ms.assetid: de54c059-cb0f-4f66-bd70-8605af05ec4f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1fe1521f2eebaa4413b49c315f17a6b1b6a5914
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/17/2019
ms.locfileid: "68887932"
---
# <a name="dimension-relationships"></a>Relazioni tra dimensioni
  L'utilizzo delle dimensioni definisce le relazioni tra le dimensioni e i gruppi di misure di un cubo. Una dimensione di un cubo è un'istanza di una dimensione del database utilizzata in un cubo specifico. Spesso un cubo contiene dimensioni che non sono correlate direttamente a un gruppo di misure, ma che possono essere correlate indirettamente al gruppo di misure tramite un'altra dimensione o un altro gruppo di misure. Quando si aggiunge una dimensione o un gruppo di misure del database a un cubo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta di determinare l'utilizzo della dimensione esaminando le relazioni tra le tabelle delle dimensioni e le tabelle dei fatti nella vista origine dati del cubo ed esaminando le relazioni tra gli attributi nelle dimensioni. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di configurare automaticamente le impostazioni delle dimensioni per le relazioni che è possibile rilevare.  
  
 Una relazione tra una dimensione e un gruppo di misure è costituita dalle tabelle delle dimensioni e dei fatti che partecipano alla relazione e da un attributo di granularità che specifica la granularità della dimensione nel particolare gruppo di misure.  
  
## <a name="regular-dimension-relationships"></a>Relazioni di tipo Regolare  
 Una relazione di tipo Regolare tra una dimensione del cubo e un gruppo di misure si verifica quando la colonna chiave della dimensione è unita in join direttamente alla tabella dei fatti. Questa relazione diretta è basata su una relazione tra chiave primaria e chiave esterna nel database relazionale sottostante, ma può anche essere basata su una relazione logica definita nella vista origine dati. Una relazione di tipo Regolare rappresenta la relazione tra le tabelle delle dimensioni e una tabella dei fatti in una progettazione con schema star tradizionale. Per ulteriori informazioni sulle relazioni regolari, vedere [definire una relazione regolare e le relative proprietà](../multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md).  
  
## <a name="reference-dimension-relationships"></a>Relazioni di tipo Riferimento  
 Una relazione di tipo Riferimento tra una dimensione del cubo e un gruppo di misure si verifica quando la colonna chiave della dimensione è unita in join direttamente alla tabella dei fatti tramite una chiave in un'altra tabella della dimensione, come illustrato nella figura seguente.  
  
 ![Diagramma logico, relazione tra dimensioni a cui si fa riferimento](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdimension1.gif "Diagramma logico, relazione tra dimensioni a cui si fa riferimento")  
  
 Una relazione di tipo Riferimento rappresenta la relazione tra le tabelle delle dimensioni e una tabella dei fatti in una progettazione con schema snowflake. Quando le tabelle delle dimensioni sono connesse in uno schema snowflake, è possibile definire una singola dimensione utilizzando colonne di più tabelle oppure definire dimensioni diverse in base a tabelle delle dimensioni separate e quindi definire un collegamento tra di esse utilizzando l'impostazione della relazione di tipo Riferimento. Nella figura seguente è illustrata una tabella dei fatti denominata **InternetSales**e due tabelle delle dimensioni denominate **Customer** e **geography**, in uno schema a fiocco di neve.  
  
 ![Schema logico, relazione tra dimensioni a cui si fa riferimento](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdim-schema1.gif "Schema logico, relazione tra dimensioni a cui si fa riferimento")  
  
 È possibile creare una dimensione con la tabella **Customer** come tabella principale della dimensione e la tabella **geography** inclusa come tabella correlata. Viene quindi definita una relazione di tipo Regolare tra la dimensione e il gruppo di misure InternetSales.  
  
 In alternativa, è possibile creare due dimensioni correlate al gruppo di misure InternetSales: una dimensione basata sulla tabella **Customer** e una dimensione basata sulla tabella **geography** . È quindi possibile correlare la dimensione Geography al gruppo di misure InternetSales utilizzando una relazione di tipo Riferimento tramite la dimensione Customer. In questo caso, quando i fatti del gruppo di misure InternetSales vengono dimensionati in base alla dimensione Geography, essi sono dimensionati in base a Customer e Geography. Se il cubo contenesse un secondo gruppo di misure denominato Reseller Sales, non sarebbe possibile dimensionare i fatti in tale gruppo di misure in base a Geography in quanto non esisterebbe alcuna relazione tra Reseller Sales e Geography.  
  
 Come illustrato nella figura seguente, non è previsto alcun limite per il numero di dimensioni di riferimento che è possibile concatenare.  
  
 ![Diagramma logico, relazione tra dimensioni a cui si fa riferimento](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdimension2.gif "Diagramma logico, relazione tra dimensioni a cui si fa riferimento")  
  
 Per ulteriori informazioni sulle relazioni a cui si fa riferimento, vedere [definire una relazione di riferimento e le proprietà delle relazioni a cui si fa riferimento](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md).  
  
## <a name="fact-dimension-relationships"></a>Relazioni di tipo Fatti  
 Le dimensioni dei fatti, spesso denominate dimensioni degenerate, sono dimensioni standard create da colonne attributo di tabelle dei fatti anziché da colonne attributo di tabelle delle dimensioni. A volte, i dati dimensionali utili vengono archiviati in una tabella dei fatti per ridurre la duplicazione. Nel diagramma seguente, ad esempio, viene visualizzata la tabella dei fatti **FactResellerSales** dal database di esempio [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)].  
  
 ![Le colonne nella tabella dei fatti possono supportare dimensioni](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-factdim.gif "Le colonne nella tabella dei fatti possono supportare dimensioni")  
  
 Nella tabella sono contenute informazioni sugli attributi non solo per ogni riga di un ordine emesso da un rivenditore, ma anche per l'ordine stesso. Gli attributi racchiusi nel diagramma precedente identificano le informazioni nella tabella **FactResellerSales** che possono essere utilizzate come attributi in una dimensione. In questo caso, due ulteriori informazioni, ovvero il numero di registrazione dello spedizioniere e il numero dell'ordine di acquisto emesso dal rivenditore, vengono rappresentate dalle colonne attributo CarrierTrackingNumber e CustomerPONumber. Queste informazioni sono interessanti. ad esempio, gli utenti sono sicuramente interessati a visualizzare informazioni aggregate, ad esempio il costo totale del prodotto, per tutti gli ordini spediti con un singolo numero di traccia. Senza una dimensione, tuttavia, non è possibile organizzare o aggregare i dati per questi due attributi.  
  
 In teoria, sarebbe possibile creare una tabella della dimensione che utilizzi le stesse informazioni chiave della tabella FactResellerSales e spostare le altre due colonne attributo, CarrierTrackingNumber e CustomerPONumber, in questa tabella. In questo modo, tuttavia, si duplicherebbe una parte significativa dei dati e si aggiungerebbe complessità superflua al data warehouse per rappresentare solo due attributi come dimensione distinta.  
  
> [!NOTE]  
>  Le dimensioni dei fatti vengono spesso utilizzate per supportare azioni drill-through. Per altre informazioni sulle azioni, vedere [Azioni &#40;Analysis Services - Dati multidimensionali&41#;](../multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Le dimensioni dei fatti devono essere aggiornate in modo incrementale dopo ogni aggiornamento del gruppo di misure cui fa riferimento la relazione di tipo Fatti. Se la dimensione dei fatti è una dimensione ROLAP, il motore di elaborazione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elimina qualsiasi cache ed elabora in modo incrementale il gruppo di misure.  
  
 Per ulteriori informazioni sulle relazioni di tipo fatti, vedere [definire una relazione di tipo fatti e le relative proprietà](../multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md).  
  
## <a name="many-to-many-dimension-relationships"></a>Relazioni molti-a-molti  
 Nella maggior parte delle dimensioni, ogni fatto si unisce in join a un solo membro della dimensione e un singolo membro della dimensione può essere associato a più fatti. Nella terminologia dei database relazionali, questa viene definita una relazione uno-a-molti. Spesso, tuttavia, può essere utile unire in join un unico fatto a più membri della dimensione. Un cliente di una banca può ad esempio avere più conti (conti correnti, conti di risparmio, carta di credito e conti titoli) e ogni conto può avere più proprietari. La dimensione relativa ai clienti creata da una relazione di questo tipo includerebbe più membri correlati a un'unica transazione relativa al conto corrente.  
  
 ![Schema logico/relazione tra dimensioni molti-a-molti](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-many-dimension1.gif "Schema logico/relazione tra dimensioni molti-a-molti")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di definire una relazione molti-a-molti tra una dimensione e una tabella dei fatti.  
  
> [!NOTE]  
>  Per supportare una relazione tra dimensioni molti-a-molti, la vista origine dati deve includere una relazione di chiave esterna tra tutte le tabelle coinvolte, come illustrato nella figura precedente. In caso contrario, non sarà possibile selezionare il gruppo di misure intermedio corretto quando si stabilisce la relazione nella scheda **Utilizzo dimensioni** di Progettazione dimensioni.  
  
 Per ulteriori informazioni sulle relazioni molti-a-molti, vedere [definire una relazione molti-a-molti e le proprietà delle relazioni molti-a-molti](../multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
