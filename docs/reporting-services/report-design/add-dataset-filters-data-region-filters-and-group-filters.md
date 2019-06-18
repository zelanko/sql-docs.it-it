---
title: Aggiungere filtri per set di dati, aree dati e gruppi | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: fcca7243-a702-4725-8e6f-cf118e988acf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d3ab6708212ce429f2abacae4353670235a687cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65582059"
---
# <a name="add-dataset-filters-data-region-filters-and-group-filters"></a>Aggiungere filtri per set di dati, aree dati e gruppi
  In un report un filtro è una parte di un set di dati, di un'area dati o di un gruppo di aree dati che viene creato per limitare i dati utilizzati nel report. I filtri consentono di controllare i dati del report se non è possibile modificare la query del set di dati, ad esempio se si utilizza un set di dati condiviso.  
  
 I filtri consentono di controllare i dati da visualizzare ed elaborare in un report. È possibile specificare filtri per un set di dati, un'area dati o un gruppo, in qualsiasi combinazione.  
  
 Per altre informazioni, vedere [Aggiungere un filtro a un set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md) ed [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="When"></a> Scelta del momento in cui impostare un filtro  
 Quando non è possibile filtrare i dati nell'origine, specificare i filtri per gli elementi del report. Utilizzare, ad esempio, i filtri di report quando l'origine dati non supporta parametri di query o quando è necessario eseguire stored procedure e non è possibile modificare la query o quando lo snapshot di un report con parametri visualizza dati personalizzati per utenti diversi.  
  
 È possibile filtrare i dati di un report prima o dopo averli recuperati da un set di dati del report. Per filtrare i dati prima che vengano recuperati, modificare la query per ogni set di dati. Quando si filtrano nella query, i dati vengono filtrati nell'origine dei dati in modo da ridurre la quantità di dati da recuperare ed elaborare in un report. Per filtrare i dati dopo che sono stati recuperati, creare espressioni di filtro nel report. È possibile impostare espressioni di filtro per un set di dati, un'area dati o un gruppo, inclusi i gruppi di dettaglio. È anche possibile includere parametri nelle espressioni di filtro, per consentire di filtrare i dati per valori o utenti specifici, ad esempio applicando un filtro su un valore che identifica l'utente che visualizza il report.  
  
##  <a name="Where"></a> Scelta della posizione in cui impostare un filtro  
 Determinare la posizione in cui impostare un filtro in base all'effetto che si desidera ottenere nel report. In fase di esecuzione, il componente Elaborazione report applica i filtri prima al set di dati, quindi all'area dati e infine ai gruppi procedendo dall'alto verso il basso in ogni gerarchia di gruppi. In una tabella, una matrice e un elenco i filtri per gruppi di righe, gruppi di colonne e gruppi adiacenti vengono applicati in modo indipendente. Anche in un grafico i filtri per gruppi di categorie e gruppi di serie vengono applicati in modo indipendente. Quando l'elaboratore di report applica il filtro, tutte le equazioni di filtro vengono applicate nell'ordine con cui sono definite nella pagina **Filtro** della finestra di dialogo **Proprietà** per ogni elemento del report. Ciò equivale a unirle alle operazioni AND booleane.  
  
 Nell'elenco seguente viene confrontato l'effetto dell'impostazione dei filtri su elementi del report differenti:  
  
-   **Set di dati** Impostare un filtro sul set di dati quando si vuole filtrare nello stesso modo una o più aree dati associate a un singolo set di dati. Impostare, ad esempio, il filtro sul set di dati associato sia a una tabella che visualizza dati di vendita che a un grafico che visualizza gli stessi dati.  
  
-   **Area dati** Impostare un filtro sull'area dati affinché una o più aree dati associate a un singolo set di dati forniscano una vista diversa del set di dati. Impostare, ad esempio, il filtro su un'area dati della tabella per visualizzare i primi dieci negozi per vendite e un'altra area dati della tabella per visualizzare gli ultimi dieci negozi per vendite nello stesso report.  
  
-   **Gruppi di righe o colonne in un'area dati Tablix** Impostare un filtro su un gruppo quando si vuole includere o escludere determinati valori per un'espressione di raggruppamento, in modo da controllare i valori di gruppo da visualizzare nella tabella, nella matrice o nell'elenco.  
  
-   **Gruppo di dettagli in un'area dati Tablix** Impostare un filtro sul gruppo di dettagli quando si dispone di più gruppi di dettagli per un'area dati e si intende visualizzare in ogni gruppo un set di dati diverso del set di dati.  
  
-   **Gruppi di serie o di categorie in un'area dati del grafico** Impostare un filtro su un gruppo di serie o di categorie quando si vuole includere o escludere determinati valori per un'espressione di raggruppamento, in modo da controllare i valori da visualizzare nel grafico.  
  
 Torna all'inizio  
  
##  <a name="FilterEquations"></a> Informazioni su un'equazione di filtro  
 In fase di esecuzione, il componente Elaborazione report converte il valore nel tipo di dati specificato, quindi utilizza l'operatore specificato per confrontare l'espressione e il valore. Nell'elenco seguente sono descritte le singole parti dell'equazione di filtro:  
  
-   **Espressione** Definisce l'elemento al quale viene applicato il filtro. In genere, corrisponde a un campo del set di dati.  
  
-   **Tipo di dati** Specifica il tipo di dati da usare quando l'equazione di filtro viene valutata dall'elaboratore di report in fase di esecuzione. Il tipo di dati che si seleziona deve essere uno dei tipi di dati supportati dallo schema di definizione del report.  
  
-   **Operatore** Definisce la modalità di confronto delle due parti dell'equazione di filtro.  
  
-   **Valore** Definisce l'espressione da usare nel confronto.  
  
 Nelle sezioni seguenti sono descritte le singole parti dell'equazione di filtro.  
  
### <a name="expression"></a>Espressione  
 Quando l'equazione di filtro viene valutata dal componente Elaborazione report in fase di esecuzione, i tipi di dati per l'espressione e il valore devono essere identici. Il tipo di dati del campo selezionato per **Espressione** viene determinato dall'estensione per l'elaborazione dati o dal provider di dati usato per recuperare i dati dall'origine dati. Il tipo di dati dell'espressione immessa per **Valore** viene determinato dai valori predefiniti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Le opzioni disponibili per il tipo di dati sono determinate dai tipi di dati supportati per una definizione del report. I valori del database potrebbero essere convertiti dal provider di dati in un tipo CLR.  
  
### <a name="data-type"></a>Tipo di dati  
 Perché il componente Elaborazione report possa confrontare due valori, è necessario che i tipi di dati siano identici. Nella tabella seguente è elencato il mapping tra tipi di dati CLR e tipi di dati della definizione del report. I dati recuperati da un'origine dati potrebbero essere convertiti in un tipo di dati diverso da quello dei dati del report.  
  
|**Tipo di dati dello schema di definizione del report**|**Tipi CLR**|  
|--------------------------------------------|-----------------------|  
|**Boolean**|**Boolean**|  
|**DateTime**|**DateTime**, **DateTimeOffset**|  
|**Integer**|**Int16**, **Int32**, **UInt16**, **Byte**, **SByte**|  
|**Float**|**Single**, **Double**, **Decimal**|  
|**Text**|**String**, **Char**, **GUID**, **Timespan**|  
  
 Quando è necessario specificare un tipo di dati, è possibile indicare la propria conversione nella parte Valore dell'espressione.  
  
### <a name="operator"></a>Operatore  
 Nella tabella seguente sono elencati gli operatori che è possibile utilizzare in un'equazione di filtro. Viene inoltre fornita la descrizione delle azioni eseguite dal componente Elaborazione report per valutare l'equazione di filtro.  
  
|Operatore|Azione|  
|--------------|------------|  
|**Equal, Like, NotEqual, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual**|Confronta l'espressione con un valore.|  
|**TopN, BottomN**|Confronta l'espressione con un valore **intero** .|  
|**TopPercent, BottomPercent**|Confronta l'espressione con un valore **intero** o **float** .|  
|**Compreso tra**|Verifica se l'espressione è compresa tra due valori (inclusi).|  
|**In**|Verifica se l'espressione è contenuta in un set di valori.|  
  
### <a name="value"></a>valore  
 L'espressione Valore specifica la parte finale dell'equazione di filtro. Il componente Elaborazione report converte l'espressione valutata nel tipo di dati specificato dall'utente, quindi valuta l'intera equazione di filtro per determinare se i dati specificati in Espressione passano attraverso il filtro.  
  
 Per eseguire la conversione in un tipo di dati diverso da un tipo di dati CLR standard, è necessario modificare l'espressione in modo da eseguire una conversione esplicita in un tipo di dati. È possibile usare le funzioni di conversione elencate nella finestra di dialogo **Espressione** in **Funzioni comuni**, **Conversione**. Ad esempio, per un campo `ListPrice` che rappresenta i dati archiviati come tipo di dati **money** in un'origine dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , l'estensione per l'elaborazione dati restituisce il valore del campo come tipo di dati <xref:System.Decimal> . Per impostare un filtro in modo da usare solo i valori maggiori di **50000,00`=CDec(50000.00)` nella valuta del report, convertire il valore in Decimal mediante l'espressione** .  
  
 Questo valore può inoltre includere un riferimento di parametro per consentire la selezione interattiva di un valore in base al quale applicare un filtro.  
  
 Torna all'inizio  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
