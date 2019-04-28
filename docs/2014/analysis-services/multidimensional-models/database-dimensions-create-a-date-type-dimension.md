---
title: Creare una dimensione di tipo Data | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time dimensions [Analysis Services]
- dimensions [Analysis Services], time
- adding time intelligence
- server time dimensions [Analysis Services]
- calendars [Analysis Services]
- time intelligence [Analysis Services]
ms.assetid: 6d692856-4b01-4dca-a650-f97ac220c114
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3eec8ddf87193eddbafc5a56e8e397c83f142a91
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726682"
---
# <a name="create-a-date-type-dimension"></a>Creare una dimensioni di tipo Date
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] una dimensione temporale è un tipo di dimensione i cui attributi rappresentano periodi di tempo, ovvero anni, semestri, trimestri, mesi e giorni. Questi periodi in una dimensione temporale offrono livelli di granularità basati sul tempo per l'analisi e la generazione di report. Gli attributi sono organizzati in gerarchie e la granularità della dimensione temporale è determinata principalmente dalle necessità aziendali e di generazione di report per i dati cronologici. Per la maggior parte dei dati finanziari e sulle vendite, ad esempio, nelle applicazioni di Business Intelligence viene utilizzata una granularità mensile o trimestrale.  
  
 In genere, nei cubi di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è inclusa una forma di dimensione temporale. Un cubo può includere più di una dimensione temporale oppure diverse gerarchie dello stesso tipo di dimensione temporale, in base ai requisiti di granularità dei dati e di generazione di report. Non tutti i cubi, tuttavia, necessitano di una dimensione temporale. Alcune applicazioni OLAP, ad esempio quelle per la determinazione dei costi in base alle attività, non richiedono una dimensione temporale, perché in questo caso la determinazione dei costi è basata sulle attività e non sul tempo.  
  
## <a name="dimension-structure"></a>Struttura dimensione  
 La struttura di una dimensione temporale dipende dalle modalità di archiviazione delle informazioni sul periodo di tempo nell'origine dei dati sottostante. La differenza nelle modalità di archiviazione comporta la creazione di due tipi di base di dimensioni temporali:  
  
 Dimensione temporale  
 Le dimensioni temporali sono simili alle altre dimensioni per il fatto che una tabella della dimensione fornisce gli attributi per la dimensione. Ogni colonna nella tabella della dimensione principale definisce un attributo per un periodo di tempo specifico.  
  
 Come con le altre dimensioni, la tabella dei fatti include una relazione di chiave esterna con la tabella della dimensione per la dimensione temporale. L'attributo chiave di una dimensione temporale è basato su una chiave integer oppure sul livello più basso di dettaglio, ad esempio la data, presente nella tabella della dimensione principale.  
  
 Dimensione temporale del server  
 Se non si dispone di una tabella della dimensione a cui associare gli attributi relativi al tempo, è possibile fare in modo che tramite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] venga definita una dimensione temporale del server basata sui periodi di tempo. Per definire gerarchie, livelli e membri rappresentati dalla dimensione temporale del server, si selezionano i periodi di tempo standard al momento della creazione della dimensione.  
  
 Gli attributi in una dimensione temporale del server presentano un'associazione tempo-attributo speciale. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa i tipi di attributo correlati alle date, ad esempio Year, Month o Day,per definire i membri degli attributi in una dimensione temporale.  
  
 Dopo avere incluso la dimensione temporale del server in un cubo, è possibile impostare la relazione tra il gruppo di misure e la dimensione temporale del server specificandola nella pagina **Definizione utilizzo delle dimensioni** della Creazione guidata cubo.  
  
### <a name="calendars"></a>Calendari  
 In una dimensione temporale o in una dimensione temporale del server gli attributi dei periodi di tempo vengono raggruppati in gerarchie. Tali gerarchie vengono in genere definite calendari.  
  
 Le applicazioni di Business Intelligence richiedono spesso più definizioni di calendari. Ad esempio, un reparto risorse umane può tenere traccia dei dipendenti usando un *standard* calendar a calendario di calendario gregoriano di dodici mesi a partire dal 1 ° gennaio e fine il 31 dicembre. Tuttavia, questo stesso reparto risorse umane può tenere traccia delle spese usando un *fiscale* calendar a calendario di dodici mesi che definisce l'anno fiscale in uso nell'organizzazione.  
  
 È possibile creare manualmente questi diversi calendari in Progettazione dimensioni. La Creazione guidata dimensione offre tuttavia diversi modelli di gerarchia che è possibile utilizzare per generare automaticamente diversi tipi di calendari quando si crea una dimensione temporale o una dimensione temporale del server. Nella tabella seguente vengono illustrati i diversi calendari che è possibile generare tramite la Creazione guidata dimensione.  
  
|Calendar|Descrizione|  
|--------------|-----------------|  
|Calendario standard|Calendario gregoriano di dodici mesi con inizio l'1 gennaio e fine il 31 dicembre.<br /><br /> Indipendentemente dal fatto che si utilizzi la Creazione guidata dimensione per creare una dimensione temporale o una dimensione temporale del server, tramite la procedura guidata viene generata una gerarchia per un calendario standard dopo che sono stati definiti gli attributi che rappresentano i periodi di tempo per la dimensione. Se si usa la Creazione guidata dimensione per creare una dimensione temporale del server, è possibile modificare la data di inizio del calendario standard impostandola su un giorno diverso rispetto all'1 gennaio.|  
|Calendario fiscale|Calendario fiscale di dodici mesi. Quando si seleziona questo calendario, è necessario specificare il giorno e il mese di inizio dell'anno fiscale in uso nell'organizzazione.<br /><br /> Nota: Questo calendario è disponibile solo se si usa la creazione guidata dimensione per creare una dimensione temporale del server.|  
|Calendario di report (o marketing)|Calendario di report di dodici mesi che include due mesi di quattro settimane e un mese di cinque settimane in un modello ripetuto di tre mesi (trimestre). Quando si seleziona questo calendario, specificare il giorno e mese e il modello di tre mesi di 4-4 e 5, 4-5-4 o 5-4-4 settimane, dove ogni cifra rappresenta il numero di settimane al mese.<br /><br /> Nota: Questo calendario è disponibile solo se si usa la creazione guidata dimensione per creare una dimensione temporale del server.|  
|Calendario produzione|Calendario che utilizza 13 periodi di quattro settimane, divisi in tre trimestri di tre periodi e un trimestre di quattro periodi. Quando si seleziona questo calendario, è necessario specificare la settimana di inizio, compresa tra 1 e 4, per l'anno di produzione in uso nell'organizzazione e identificare inoltre quale trimestre include quattro periodi.<br /><br /> Nota: Questo calendario è disponibile solo se si usa la creazione guidata dimensione per creare una dimensione temporale del server.|  
|Calendario ISO 8601|Calendario standard ISO (International Organization for Standardization) per il formato della data e dell'ora (8601). Calendario costituito da un numero intero di settimane di sette giorni. L'anno può iniziare alcuni giorni prima o dopo l'inizio del nuovo anno in base al calendario gregoriano. La prima settimana del calendario è determinata dalla prima settimana del calendario gregoriano contenente un giovedì. Il primo giorno di questa settimana, pertanto, può trovarsi nell'anno precedente.<br /><br /> Nota: Questo calendario è disponibile solo se si usa la creazione guidata dimensione per creare una dimensione temporale del server.|  
  
 Quando si crea una dimensione temporale del server e si specificano i periodi di tempo e i calendari da utilizzare nella dimensione, tramite la Creazione guidata dimensione vengono aggiunti gli attributi per i periodi di tempo appropriati per ogni calendario specificato. Se si crea, ad esempio, una dimensione temporale del server in cui come periodo di tempo vengono utilizzati gli anni e che include sia un calendario fiscale che un calendario di report, tramite la procedura guidata vengono aggiunti alla dimensione gli attributi FiscalYear e ReportingYears, oltre all'attributo standard Years. Una dimensione temporale del server dispone inoltre di attributi per le combinazioni dei periodi di tempo selezionati, ad esempio un attributo DayOfWeek per una dimensione contenente i livelli Giorni e Settimane. Tramite la Creazione guidata dimensione viene creata una gerarchia del calendario combinando gli attributi appartenenti a un singolo tipo di calendario. Ad esempio, una gerarchia di calendario fiscale può includere i livelli seguenti: L'anno fiscale, Semestre fiscale dell'anno, trimestre fiscale, mese fiscale e giorno fiscale.  
  
## <a name="adding-time-intelligence-with-the-business-intelligence-wizard"></a>Aggiunta di funzionalità di Business Intelligence per le gerarchie temporali tramite la Configurazione guidata funzionalità di Business Intelligence  
 Dopo avere definito una dimensione temporale e averla aggiunta a un cubo, è possibile utilizzare la Configurazione guidata funzionalità di Business Intelligence per aggiungere funzionalità di Business Intelligence per le gerarchie temporali, ad esempio misure per il calcolo dei dati di un periodo rispetto alla data corrente, di un periodo specifico o della media mobile dei dati in un periodo. Per altre informazioni [Definire calcoli delle funzionalità di Business Intelligence per le gerarchie temporali mediante la Configurazione guidata funzionalità di Business Intelligence](define-time-intelligence-calculations-using-the-business-intelligence-wizard.md).  
  
> [!NOTE]  
>  Non è possibile utilizzare la Configurazione guidata funzionalità di Business Intelligence per aggiungere funzionalità di Business Intelligence per le gerarchie temporali alle dimensioni temporali del server. Tramite la Configurazione guidata funzionalità di Business Intelligence viene aggiunta una gerarchia per supportare le funzionalità di Business Intelligence per le gerarchie temporali e tale gerarchia deve essere associata a una colonna della tabella della dimensione temporale. Le dimensioni temporali del server non dispongono di una tabella della dimensione temporale corrispondente e pertanto non supportano questa gerarchia aggiuntiva.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Time Dimension by Generating a Time Table](create-a-time-dimension-by-generating-a-time-table.md)   
 [Guida sensibile al contesto della Configurazione guidata funzionalità di Business Intelligence](../business-intelligence-wizard-f1-help.md)   
 [Tipi di dimensioni](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
