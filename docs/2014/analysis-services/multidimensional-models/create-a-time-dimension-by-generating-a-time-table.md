---
title: Creare una dimensione temporale generando una tabella dei tempi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time dimensions [Analysis Services]
- dimensions [Analysis Services], time
- time periods [Analysis Services]
- range-based time dimensions [Analysis Services]
- server time dimensions [Analysis Services]
- calendars [Analysis Services]
- table-based time dimensions [Analysis Services]
ms.assetid: 58303326-1361-4c0e-9f3d-642ce69c4f6a
author: minewiskan
ms.author: owend
ms.openlocfilehash: af1cc0c5838c942d8f04eb5246c9c1714d08d786
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84536463"
---
# <a name="create-a-time-dimension-by-generating-a-time-table"></a>Create a Time Dimension by Generating a Time Table
  In è [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] possibile utilizzare la creazione guidata dimensione in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per creare una dimensione temporale quando non sono disponibili tabelle temporali nel database di origine. È possibile eseguire questa operazione selezionando una delle opzioni seguenti nella pagina **Seleziona metodo di creazione** :  
  
-   Se si dispone delle autorizzazioni per creare oggetti nell'origine dati sottostante, utilizzare l'opzione**Genera una tabella dei tempi nell'origine dei dati** . La procedura guidata consente di generare una tabella dei tempi e di archiviare questa tabella nell'origine dati. La procedura guidata consente di creare la dimensione temporale dalla tabella dei tempi.  
  
-   Se si dispone delle autorizzazioni per creare oggetti nell'origine dati sottostante, utilizzare l'opzione**Genera una tabella dei tempi sul server** . La procedura guidata consente di generare e archiviare una tabella sul server invece che nell'origine dati. (La dimensione creata da una tabella dei tempi nel server è denominata *dimensione temporale del server*.) La procedura guidata consente di creare la dimensione temporale del server da questa tabella.  
  
 Quando si crea una dimensione temporale, si specificano i periodi di tempo nonché le date di inizio e di fine della dimensione. I periodi di tempo specificati verranno utilizzati dalla procedura guidata per creare gli attributi temporali. Quando si elabora la dimensione, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera e archivia i dati per il supporto delle date e dei periodi specificati. La procedura guidata utilizza gli attributi creati per una dimensione temporale per suggerire gerarchie per la dimensione. Tali gerarchie si basano sulle relazioni esistenti tra diversi periodi di tempo e tengono conto di diversi calendari. Ad esempio, in una gerarchia con il calendario standard un livello delle settimane appare sotto un livello degli anni ma non sotto un livello dei mesi perché le settimane vengono suddivise in modo uniforme tra gli anni ma non tra i mesi. In una gerarchia con il calendario di produzione o report, invece, le settimane vengono suddivise in modo uniforme tra i mesi, pertanto un livello delle settimane viene visualizzato sotto un livello dei mesi.  
  
## <a name="define-time-periods"></a>Definizione dei periodi di tempo  
 Utilizzare la pagina **Definizione periodi di tempo** della procedura guidata per specificare l'intervallo di date che si desidera includere nella dimensione. È ad esempio possibile selezionare un intervallo che decorre dal primo gennaio del primo anno a cui si riferiscono i dati e che termina uno o due anni dopo l'anno corrente per consentire transazioni future. Le transazioni che non rientrano in questo intervallo non verranno visualizzate oppure verranno visualizzate come membri sconosciuti nella dimensione in base all'impostazione della proprietà `UnknownMemberVisible` della dimensione. È inoltre possibile modificare il primo giorno della settimana utilizzato nei dati. Il giorno predefinito è domenica.  
  
 Selezionare i periodi di tempo quando la procedura guidata crea le gerarchie applicabili ai dati, ad esempio gli anni, i semestri, i trimestri, i quadrimestri, i mesi, le decadi, le settimane o una data. È necessario selezionare sempre almeno il periodo di tempo Data. L'attributo Data è l'attributo chiave della dimensione e senza di esso la dimensione non può funzionare.  
  
 Accanto a **Lingua per i nomi dei membri della dimensione temporale**selezionare la lingua da utilizzare nelle etichette dei membri della dimensione.  
  
 Dopo avere creato una dimensione temporale basata su un intervallo di date, è possibile utilizzare Progettazione dimensioni per aggiungere o rimuovere attributi temporali. L'attributo Data non può essere rimosso perché è l'attributo chiave della dimensione. Per nascondere l'attributo Data in modo che non venga visualizzato agli utenti, è possibile modificare la proprietà `AttributeHierarchyVisible` sull'attributo in `False`.  
  
## <a name="select-calendars"></a>Selezione dei calendari  
 Quando si crea una dimensione temporale, viene sempre incluso il calendario standard di 12 mesi (gregoriano), che ha inizio il primo gennaio e termina il 31 dicembre. Nella pagina **Selezione calendari** della procedura guidata è possibile specificare altri calendari su cui basare le gerarchie della dimensione. Per le descrizioni dei tipi di calendario, vedere [Creare una dimensioni di tipo Date](database-dimensions-create-a-date-type-dimension.md).  
  
 Gli attributi creati nella dimensione dipendono dai periodi di tempo selezionati nella pagina **Definizione periodi di tempo** della procedura guidata e dalle opzioni selezionate per il calendario. Se, ad esempio, si selezionano i periodi di tempo **Anno** e **Trimestre** nella pagina **Definizione periodi di tempo** della procedura guidata e il tipo di calendario **Calendario fiscale** nella pagina **Selezione calendari** , per il calendario fiscale verranno creati automaticamente gli attributi FiscalYear, FiscalQuarter e FiscalQuarterOfYear.  
  
 La procedura guidata crea inoltre gerarchie specifiche del calendario composte da attributi creati per il calendario. Per ogni calendario, ogni livello di ogni gerarchia è sottoposto al rollup nel livello superiore. Ad esempio, nel calendario standard di 12 mesi la procedura guidata crea una gerarchia con anni e settimane o anni e mesi. Le settimane non sono però ripartite in modo uniforme tra i mesi di un calendario standard, pertanto non esiste una gerarchia con anni, mesi e settimane. Viceversa, in un calendario di report o produzione le settimane sono suddivise in modo uniforme tra i mesi, pertanto viene eseguito il rollup delle settimane nei mesi.  
  
## <a name="completing-the-dimension-wizard"></a>Completamento di Creazione guidata dimensione  
 Nella pagina **Completamento procedura guidata** controllare gli attributi e le gerarchie creati dalla procedura guidata e quindi assegnare un nome alla dimensione temporale. Fare clic su **Fine** per completare la procedura guidata e creare la dimensione. Dopo avere completato la dimensione, è possibile modificarla in Progettazione dimensioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md)   
 [Creare una dimensione di tipo data](database-dimensions-create-a-date-type-dimension.md)   
 [Proprietà delle dimensioni del database](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [Relazioni tra dimensioni](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Creare una dimensione utilizzando una tabella esistente](create-a-dimension-by-using-an-existing-table.md)   
 [Creare una dimensione generando una tabella non temporale nell'origine dati](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
