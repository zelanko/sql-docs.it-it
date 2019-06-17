---
title: Creare una dimensione temporale generando una tabella temporale | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d35cf55f64b977e952b57416a31c35cd669fc468
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867055"
---
# <a name="create-a-time-dimension-by-generating-a-time-table"></a>Create a Time Dimension by Generating a Time Table
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è possibile usare Creazione guidata dimensione in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per creare una dimensione temporale quando non sono disponibili tabelle tempo nel database di origine. È possibile eseguire questa operazione selezionando una delle opzioni seguenti nella pagina **Seleziona metodo di creazione** :  
  
-   Se si dispone delle autorizzazioni per creare oggetti nell'origine dati sottostante, utilizzare l'opzione**Genera una tabella dei tempi nell'origine dei dati** . La procedura guidata consente di generare una tabella dei tempi e di archiviare questa tabella nell'origine dati. La procedura guidata consente di creare la dimensione temporale dalla tabella dei tempi.  
  
-   Se si dispone delle autorizzazioni per creare oggetti nell'origine dati sottostante, utilizzare l'opzione**Genera una tabella dei tempi sul server** . La procedura guidata consente di generare e archiviare una tabella sul server invece che nell'origine dati. (La dimensione creata da una tabella dei tempi nel server è denominata *dimensione temporale del server*.) La procedura guidata consente di creare la dimensione temporale del server da questa tabella.  
  
 Quando si crea una dimensione temporale, si specificano i periodi di tempo nonché le date di inizio e di fine della dimensione. I periodi di tempo specificati verranno utilizzati dalla procedura guidata per creare gli attributi temporali. Quando si elabora la dimensione, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera e archivia i dati per il supporto delle date e dei periodi specificati. La procedura guidata utilizza gli attributi creati per una dimensione temporale per suggerire gerarchie per la dimensione. Tali gerarchie si basano sulle relazioni esistenti tra diversi periodi di tempo e tengono conto di diversi calendari. Ad esempio, in una gerarchia con il calendario standard un livello delle settimane appare sotto un livello degli anni ma non sotto un livello dei mesi perché le settimane vengono suddivise in modo uniforme tra gli anni ma non tra i mesi. In una gerarchia con il calendario di produzione o report, invece, le settimane vengono suddivise in modo uniforme tra i mesi, pertanto un livello delle settimane viene visualizzato sotto un livello dei mesi.  
  
## <a name="define-time-periods"></a>Definizione dei periodi di tempo  
 Utilizzare la pagina **Definizione periodi di tempo** della procedura guidata per specificare l'intervallo di date che si desidera includere nella dimensione. È ad esempio possibile selezionare un intervallo che decorre dal primo gennaio del primo anno a cui si riferiscono i dati e che termina uno o due anni dopo l'anno corrente per consentire transazioni future. Le transazioni che non rientrano in questo intervallo non verranno visualizzate oppure verranno visualizzate come membri sconosciuti nella dimensione in base all'impostazione della proprietà **UnknownMemberVisible** della dimensione. È inoltre possibile modificare il primo giorno della settimana utilizzato nei dati. Il giorno predefinito è domenica.  
  
 Selezionare i periodi di tempo quando la procedura guidata crea le gerarchie applicabili ai dati, ad esempio gli anni, i semestri, i trimestri, i quadrimestri, i mesi, le decadi, le settimane o una data. È necessario selezionare sempre almeno il periodo di tempo Data. L'attributo Data è l'attributo chiave della dimensione e senza di esso la dimensione non può funzionare.  
  
 Accanto a **Lingua per i nomi dei membri della dimensione temporale**selezionare la lingua da utilizzare nelle etichette dei membri della dimensione.  
  
 Dopo avere creato una dimensione temporale basata su un intervallo di date, è possibile utilizzare Progettazione dimensioni per aggiungere o rimuovere attributi temporali. L'attributo Data non può essere rimosso perché è l'attributo chiave della dimensione. Per nascondere l'attributo Data agli utenti, è possibile modificare la proprietà **AttributeHierarchyVisible** dell'attributo in **False**.  
  
## <a name="select-calendars"></a>Selezione dei calendari  
 Quando si crea una dimensione temporale, viene sempre incluso il calendario standard di 12 mesi (gregoriano), che ha inizio il primo gennaio e termina il 31 dicembre. Nella pagina **Selezione calendari** della procedura guidata è possibile specificare altri calendari su cui basare le gerarchie della dimensione. Per le descrizioni dei tipi di calendario, vedere [Creare una dimensioni di tipo Date](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md).  
  
 Gli attributi creati nella dimensione dipendono dai periodi di tempo selezionati nella pagina **Definizione periodi di tempo** della procedura guidata e dalle opzioni selezionate per il calendario. Se, ad esempio, si selezionano i periodi di tempo **Anno** e **Trimestre** nella pagina **Definizione periodi di tempo** della procedura guidata e il tipo di calendario **Calendario fiscale** nella pagina **Selezione calendari** , per il calendario fiscale verranno creati automaticamente gli attributi FiscalYear, FiscalQuarter e FiscalQuarterOfYear.  
  
 La procedura guidata crea inoltre gerarchie specifiche del calendario composte da attributi creati per il calendario. Per ogni calendario, ogni livello di ogni gerarchia è sottoposto al rollup nel livello superiore. Ad esempio, nel calendario standard di 12 mesi la procedura guidata crea una gerarchia con anni e settimane o anni e mesi. Le settimane non sono però ripartite in modo uniforme tra i mesi di un calendario standard, pertanto non esiste una gerarchia con anni, mesi e settimane. Viceversa, in un calendario di report o produzione le settimane sono suddivise in modo uniforme tra i mesi, pertanto viene eseguito il rollup delle settimane nei mesi.  
  
## <a name="completing-the-dimension-wizard"></a>Completamento di Creazione guidata dimensione  
 Nella pagina **Completamento procedura guidata** controllare gli attributi e le gerarchie creati dalla procedura guidata e quindi assegnare un nome alla dimensione temporale. Fare clic su **Fine** per completare la procedura guidata e creare la dimensione. Dopo avere completato la dimensione, è possibile modificarla in Progettazione dimensioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Creare una dimensioni di tipo Date](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md)   
 [Proprietà delle dimensioni del database](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [Relazioni tra dimensioni](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Creare una dimensione generando una tabella non temporale nell'origine dati](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
