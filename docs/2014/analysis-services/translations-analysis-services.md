---
title: Traduzioni (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence Development Studio, translations [Analysis Services]
- translations [Analysis Services], about translations
- object translations [Analysis Services]
- language identifiers [Analysis Services]
- attribute translations [Analysis Services]
- translations [Analysis Services]
ms.assetid: 018471e0-3c82-49ec-aa16-467fb58a6d5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e85f6ca82f11b9f19c14a020d879afb65a6d1775
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62794482"
---
# <a name="translations-analysis-services"></a>Traduzioni (Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]**  Solo dati multidimensionali  
  
 In un modello di dati multidimensionale di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è possibile incorporare più traduzioni di una didascalia per fornire stringhe specifiche delle impostazioni locali in base all'identificatore LCID. È possibile aggiungere traduzioni per il nome del database, gli oggetti cubo e gli oggetti dimensione del database.  
  
 La definizione di una traduzione crea i metadati e la didascalia tradotta all'interno del modello, ma per eseguire il rendering delle stringhe localizzate in un'applicazione client, è necessario impostare la proprietà `Language` per l'oggetto o passare un parametro `Locale Identifier` nella stringa di connessione, impostando ad esempio `LocaleIdentifier=1036` per restituire le stringhe francesi. Pensare di usare `Locale Identifier` se si vuole supportare più traduzioni simultanee dello stesso oggetto in lingue diverse. L'impostazione della proprietà `Language` funziona, ma influisce anche sull'elaborazione e l'esecuzione di query comportando conseguenze impreviste. È preferibile scegliere di impostare il parametro `Locale Identifier` in quanto viene usato solo per restituire le stringhe tradotte.  
  
 Una traduzione è costituita da un identificatore delle impostazioni locali (LCID), una didascalia tradotta per l'oggetto (ad esempio, il nome di una dimensione o di un attributo), e facoltativamente un'associazione a una colonna che fornisce i valori dei dati nella lingua di destinazione. È possibile avere più traduzioni, ma è possibile usarne solo una per ogni connessione specifica. In teoria, non vi sono limiti al numero di traduzioni che è possibile incorporare nel modello, ma ogni traduzione aggiunge complessità al test e tutte le traduzioni devono condividere le stesse regole di confronto, pertanto quando si progetta la soluzione tenere presenti questi vincoli normali.  
  
> [!TIP]  
>  È possibile usare le applicazioni client quali Excel, Management Studio e [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] per restituire le stringhe tradotte. Per informazioni dettagliate, vedere [Globalization Tips and Best Practices &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) .  
  
## <a name="setting-up-a-model-to-support-translated-members"></a>Configurazione di un modello per supportare i membri tradotti  
 Un modello di dati usato in una soluzione multilingue non richiede solo le etichette tradotte (nomi di campo e descrizioni), ma è necessario fornire anche i valori dei dati articolati in vari alfabeti. Per ottenere una soluzione multilingue è necessario che i singoli attributi associati alle colonne in un database esterno restituiscano i dati.  
  
 I database di esempio Adventure Works (multidimensionale e data warehouse relazionale) illustrano la funzionalità di traduzione. Il modello di esempio include didascalie e descrizioni tradotte. Il data warehouse relazionale di esempio contiene le colonne dei valori tradotti che forniscono i membri degli attributi localizzati nel modello.  
  
 Per visualizzare i valori dei dati tradotti disponibili per il modello:  
  
1.  Aprire il modello multidimensionale Adventure Works nella finestra di progettazione.  
  
2.  In Esplora soluzioni aprire viste origine dati e fare doppio clic su Adventure Works DW\<versione > DSV.  
  
3.  Trovare dimDate, dimProduct, dimProductCategory o dimProductSubcateogry. Tutte queste dimensioni contengono gli attributi dei membri tradotti per mese, giorno della settimana, nome del prodotto, nome della categoria e così via.  
  
4.  Fare clic con il pulsante destro del mouse su un campo qualsiasi e scegliere **Esplora dati**. Verranno visualizzare le traduzione in inglese, spagnolo e francese di ciascun membro.  
  
 I formati di data, ora e valuta non vengono implementati tramite le traduzioni. Per fornire in modo dinamico i formati specifici della lingua in base alle impostazioni locali del client, usare la Conversione guidata valuta e la proprietà `FormatString`. Per informazioni dettagliate, vedere [Conversioni di valuta &#40;Analysis Services&#41;](currency-conversions-analysis-services.md) ed [Elemento FormatString &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/formatstring-element-assl).  
  
 [Lezione 9: Definizione di prospettive e traduzioni](lesson-9-defining-perspectives-and-translations.md) nelle esercitazioni su Analysis Services illustrerà i passaggi per creare e testare le traduzioni.  
  
## <a name="defining-translations"></a>Definizione di traduzioni  
 La definizione di una traduzione crea un oggetto `Translation` come elemento figlio dell'oggetto cubo, dimensione o database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Usare [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] per aprire la soluzione e definire le traduzioni.  
  
### <a name="add-translations-to-a-cube"></a>Aggiungere le traduzioni a un cubo  
 È possibile aggiungere le traduzioni al cubo, ai gruppi di misure, alle misure, alla dimensione del cubo, alle prospettive, agli indicatori KPI, alle azioni, ai set denominati e ai membri calcolati.  
  
1.  In Esplora soluzioni fare doppio clic sul nome del cubo per aprire Progettazione cubi.  
  
2.  Fare clic sulla scheda **Traduzioni** . In questa pagina vengono elencati tutti gli oggetti che supportano le traduzioni.  
  
3.  Per ogni oggetto specificare la lingua di destinazione (viene risolta internamente in un LCID), la didascalia tradotta e la descrizione tradotta. L'elenco delle lingue è coerente in Analysis Services, sia che si imposti la lingua del server in Management Studio sia che si aggiunga un override della traduzione per un singolo attributo.  
  
     Tenere presente che non è possibile modificare le regole di confronto. Un cubo usa essenzialmente un set di regole di confronto, anche se vengono supportate più lingue tramite le didascalie tradotte (è prevista un'eccezione per gli attributi della dimensione, descritta di seguito). Se le lingue non vengono ordinate correttamente nelle regole di confronto condivise, sarà necessario eseguire delle copie del cubo per poter soddisfare i requisiti delle regole di confronto.  
  
4.  Compilare e distribuire il progetto.  
  
5.  Connettersi al database tramite un'applicazione client, ad esempio Excel, modificando la stringa di connessione in modo da usare l'identificatore delle impostazioni locali. Per informazioni dettagliate, vedere [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) .  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>Aggiungere le traduzioni per una dimensione e gli attributi  
 È possibile aggiungere le traduzioni per le dimensioni del database, gli attributi, le gerarchie e i livelli all'interno di una gerarchia.  
  
 Le didascalie tradotte vengono aggiunte al modello manualmente usando la tastiera o la funzione di copia e incolla, mentre per i membri degli attributi della dimensione è possibile ottenere i valori tradotti da un database esterno. In particolare, è possibile associare la proprietà `CaptionColumn` di un attributo a una colonna in una vista origine dati.  
  
 A livello di attributo è possibile eseguire l'override delle impostazioni delle regole di confronto per poter ad esempio modificare la distinzione di larghezza o usare un ordinamento binario per un attributo specifico. In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]le regole di confronto sono presenti dove vengono definiti i data binding. Poiché si sta associando una traduzione dell'attributo della dimensione a una colonna di origine diversa nella vista origine dati, è disponibile un'impostazione delle regole di confronto in modo da poter specificare le regole di confronto usate dalla colonna di origine. Per informazioni sulle regole di confronto delle colonne nel database relazionale, vedere [Set or Change the Column Collation](../relational-databases/collations/set-or-change-the-column-collation.md) .  
  
1.  In Esplora soluzioni fare doppio clic sul nome della dimensione per aprire Progettazione dimensioni.  
  
2.  Fare clic sulla scheda **Traduzioni** . In questa pagina sono elencati tutti gli oggetti dimensione che supportano le traduzioni.  
  
     Per ogni oggetto specificare la lingua di destinazione (viene risolta in un LCID), la didascalia tradotta e la descrizione tradotta. L'elenco delle lingue è coerente in Analysis Services, sia che si imposti la lingua del server in Management Studio sia che si aggiunga un override della traduzione per un singolo attributo.  
  
3.  Per associare un attributo a una colonna che fornisce valori tradotti:  
  
    1.  In Progettazione dimensioni | **Traduzioni**aggiungere una nuova traduzione. Scegliere la lingua. Una nuova colonna verrà visualizzata nella pagina per accettare i valori tradotti.  
  
    2.  Posizionare il cursore in una cella vuota accanto a quella degli attributi. L'attributo non può essere la chiave, ma tutti gli altri attributi sono scelte possibili. Verrà visualizzato un piccolo pulsante con un punto. Fare clic sul pulsante per aprire la finestra di dialogo **Traduzione dati attributo**.  
  
    3.  Immettere una traduzione per la didascalia. Verrà usata come etichetta dati nella lingua di destinazione, ad esempio come nome di campo in un elenco di campi della tabella pivot.  
  
    4.  Scegliere la colonna di origine che fornisce i valori tradotti dei membri dell'attributo. Sono disponibili solo le colonne preesistenti nella tabella o nella query associata alla dimensione. Se la colonna non esiste, è necessario modificare la vista origine dati, la dimensione e il cubo per visualizzare la colonna.  
  
    5.  Scegliere le regole di confronto e l'ordinamento, se applicabile.  
  
4.  Compilare e distribuire il progetto.  
  
5.  Connettersi al database tramite un'applicazione client, ad esempio Excel, modificando la stringa di connessione in modo da usare l'identificatore delle impostazioni locali. Per informazioni dettagliate, vedere [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md).  
  
### <a name="add-a-translation-of-the-database-name"></a>Aggiungere una traduzione del nome del database  
 A livello di database, è possibile aggiungere le traduzioni per il nome e la descrizione del database. Il nome del database tradotto potrebbe essere visibile nelle connessioni client che specificano l'identificatore LCID della lingua, ma questo dipende dallo strumento. Ad esempio, se si visualizza il database in Management Studio il nome tradotto non sarà visibile anche se si specifica l'identificatore delle impostazioni locali per la connessione. L'API usata da Management Studio per connettersi ad Analysis Services non legge la proprietà `Language`.  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul nome del progetto | **Modifica database** per aprire la finestra Progettazione database.  
  
2.  In Traduzioni specificare la lingua di destinazione (viene risolta in un LCID), la didascalia tradotta e la descrizione tradotta. L'elenco delle lingue è coerente in Analysis Services, sia che si imposti la lingua del server in Management Studio sia che si aggiunga un override della traduzione per un singolo attributo.  
  
3.  Nella pagina delle proprietà del database impostare `Language` sullo stesso LCID specificato per la traduzione. Facoltativamente, impostare anche `Collation` se il valore predefinito non è più adatto.  
  
4.  Compilare e distribuire il database.  
  
## <a name="resolving-translations"></a>Risoluzione di traduzioni  
 Se un'applicazione client richiede un identificatore delle impostazioni locali, l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tenta di risolvere i dati e metadati per gli oggetti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] con l'identificatore LCID corrispondente più vicino. Se l'applicazione client non specifica una lingua predefinita oppure specifica l'identificatore delle impostazioni locali neutro (0) o l'identificatore della lingua predefinita (1024), [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] restituisce i dati e i metadati per l'oggetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nella lingua predefinita.  
  
## <a name="see-also"></a>Vedere anche  
 [Scenari di globalizzazione per Analysis Services multidimensionale](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [Lingue e regole di confronto &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)   
 [Impostare o modificare le regole di confronto delle colonne](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)  
  
  
