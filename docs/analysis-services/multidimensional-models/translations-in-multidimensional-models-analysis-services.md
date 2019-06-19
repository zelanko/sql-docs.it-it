---
title: Traduzioni nei modelli multidimensionali (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f25023f6a0191cb645134d327f40ea84ba64932f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65357307"
---
# <a name="translations-in-multidimensional-models-analysis-services"></a>Traduzioni nei modelli multidimensionali (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  È possibile definire le traduzioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mediante la finestra di progettazione appropriata per l'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da tradurre. Mediante la definizione di una traduzione viene creato un oggetto **Translation** associato all'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] appropriato con i valori letterali espliciti specificati, nella lingua indicata, per le proprietà dell'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] correlato.  
  
## <a name="elements-of-a-multi-lingual-data-model"></a>Elementi di un modello di dati multilingue  
 Un modello di dati usato in una soluzione multilingue non richiede solo le etichette tradotte (nomi di campo e descrizioni), ma è necessario fornire anche i valori dei dati articolati in vari alfabeti. Per ottenere una soluzione multilingue è necessario che i singoli attributi associati alle colonne in un database esterno restituiscano i dati.  
  
 I database di esempio Adventure Works (multidimensionale e data warehouse relazionale) illustrano la funzionalità di traduzione di Analysis Services. Il modello di esempio include didascalie e descrizioni tradotte. Il data warehouse relazionale di esempio contiene le colonne dei valori tradotti che forniscono i membri degli attributi localizzati nel modello.  
  
 Per visualizzare i valori dei dati tradotti disponibili per il modello:  
  
1.  Aprire il modello multidimensionale Adventure Works nella finestra di progettazione.  
  
2.  In Esplora soluzioni aprire viste origine dati e fare doppio clic su Adventure Works DW\<versione > DSV.  
  
3.  Trovare dimDate, dimProduct, dimProductCategory o dimProductSubcateogry. Tutte queste dimensioni contengono gli attributi dei membri tradotti per mese, giorno della settimana, nome del prodotto, nome della categoria e così via.  
  
4.  Fare clic con il pulsante destro del mouse su un campo qualsiasi e scegliere **Esplora dati**. Verranno visualizzare le traduzione in inglese, spagnolo e francese di ciascun membro.  
  
 I formati di data, ora e valuta non vengono implementati tramite le traduzioni. Per fornire in modo dinamico i formati specifici della lingua in base alle impostazioni locali del client, usare la Conversione guidata valuta e la proprietà **FormatString** . Per informazioni dettagliate, vedere [Conversioni di valuta &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md) ed [Elemento FormatString &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/formatstring-element-assl).  
  
## <a name="defining-translations"></a>Definizione di traduzioni  
  
### <a name="add-translations-to-a-cube"></a>Aggiungere le traduzioni a un cubo  
 È possibile aggiungere le traduzioni al cubo, ai gruppi di misure, alle misure, alla dimensione del cubo, alle prospettive, agli indicatori KPI, alle azioni, ai set denominati e ai membri calcolati.  
  
1.  In Esplora soluzioni fare doppio clic sul nome del cubo per aprire Progettazione cubi.  
  
2.  Fare clic sulla scheda **Traduzioni** . In questa pagina vengono elencati tutti gli oggetti che supportano le traduzioni.  
  
3.  Per ogni oggetto specificare la lingua di destinazione (viene risolta internamente in un LCID), la didascalia tradotta e la descrizione tradotta. L'elenco delle lingue è coerente in Analysis Services, sia che si imposti la lingua del server in Management Studio sia che si aggiunga un override della traduzione per un singolo attributo.  
  
     Tenere presente che non è possibile modificare le regole di confronto. Un cubo usa essenzialmente un set di regole di confronto, anche se vengono supportate più lingue tramite le didascalie tradotte (è prevista un'eccezione per gli attributi della dimensione, descritta di seguito). Se le lingue non vengono ordinate correttamente nelle regole di confronto condivise, sarà necessario eseguire delle copie del cubo per poter soddisfare i requisiti delle regole di confronto.  
  
4.  Compilare e distribuire il progetto.  
  
5.  Connettersi al database tramite un'applicazione client, ad esempio Excel, modificando la stringa di connessione in modo da usare l'identificatore delle impostazioni locali. Per informazioni dettagliate, vedere [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md) .  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>Aggiungere le traduzioni per una dimensione e gli attributi  
 È possibile aggiungere le traduzioni per le dimensioni del database, gli attributi, le gerarchie e i livelli all'interno di una gerarchia.  
  
 Le didascalie tradotte vengono aggiunte al modello manualmente usando la tastiera o la funzione di copia e incolla, mentre per i membri degli attributi della dimensione è possibile ottenere i valori tradotti da un database esterno. In particolare, è possibile associare la proprietà **CaptionColumn** di un attributo a una colonna in una vista origine dati.  
  
 A livello di attributo è possibile eseguire l'override delle impostazioni delle regole di confronto per poter ad esempio modificare la distinzione di larghezza o usare un ordinamento binario per un attributo specifico. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]le regole di confronto sono presenti dove vengono definiti i data binding. Poiché si sta associando una traduzione dell'attributo della dimensione a una colonna di origine diversa nella vista origine dati, è disponibile un'impostazione delle regole di confronto in modo da poter specificare le regole di confronto usate dalla colonna di origine. Per informazioni sulle regole di confronto delle colonne nel database relazionale, vedere [Set or Change the Column Collation](../../relational-databases/collations/set-or-change-the-column-collation.md) .  
  
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
  
5.  Connettersi al database tramite un'applicazione client, ad esempio Excel, modificando la stringa di connessione in modo da usare l'identificatore delle impostazioni locali. Per informazioni dettagliate, vedere [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md).  
  
### <a name="add-a-translation-of-the-database-name"></a>Aggiungere una traduzione del nome del database  
 A livello di database, è possibile aggiungere le traduzioni per il nome e la descrizione del database. Il nome del database tradotto potrebbe essere visibile nelle connessioni client che specificano l'identificatore LCID della lingua, ma questo dipende dallo strumento. Ad esempio, se si visualizza il database in Management Studio il nome tradotto non sarà visibile anche se si specifica l'identificatore delle impostazioni locali per la connessione. L'API usata da Management Studio per connettersi ad Analysis Services non legge la proprietà **Language** .  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul nome del progetto | **Modifica database** per aprire la finestra Progettazione database.  
  
2.  In Traduzioni specificare la lingua di destinazione (viene risolta in un LCID), la didascalia tradotta e la descrizione tradotta. L'elenco delle lingue è coerente in Analysis Services, sia che si imposti la lingua del server in Management Studio sia che si aggiunga un override della traduzione per un singolo attributo.  
  
3.  Nella pagina delle proprietà del database impostare **Language** sullo stesso LCID specificato per la traduzione. Facoltativamente, impostare anche **Collation** se il valore predefinito non è più adatto.  
  
4.  Compilare e distribuire il database.  
  
## <a name="deleting-translation-objects"></a>Eliminazione di oggetti Translation  
 È possibile fare clic con il pulsante destro del mouse su un oggetto di questo tipo in Progettazione dimensioni o Progettazione cubi per rimuoverlo definitivamente. Non è possibile ripristinare o riciclare un oggetto eliminato, quindi è opportuno accertarsi di controllare l'elenco degli oggetti interessati prima di continuare.  
  
## <a name="resolving-translations"></a>Risoluzione di traduzioni  
 Se un'applicazione client richiede informazioni corrispondenti all'identificatore di lingua specificato, l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta di risolvere i dati e i metadati per gli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] approssimandoli all'identificatore di lingua più vicino. Se l'applicazione client non specifica una lingua predefinita oppure specifica l'identificatore delle impostazioni locali neutro (0) o l'identificatore della lingua predefinita (1024), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce i dati e i metadati per l'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nella lingua predefinita.  
  
 Se l'applicazione client specifica un identificatore di lingua diverso da quello della lingua predefinita, l'istanza scorre tutte le traduzioni disponibili per tutti gli oggetti disponibili. Se l'identificatore di lingua specificato corrisponde all'identificatore di lingua di una traduzione, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce tale traduzione. Nel caso in cui non sia possibile trovare una corrispondenza, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta di utilizzare uno dei metodi seguenti per restituire l'identificatore di lingua più vicino a quello specificato.  
  
-   Per gli identificatori di lingua seguenti, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta di utilizzare un identificatore di lingua alternativo se non è stata definita una traduzione per l'identificatore di lingua specificato:  
  
    |Identificatore di lingua specificato|Identificatore di lingua alternativo|  
    |-----------------------------------|-----------------------------------|  
    |3076 - Cinese (RAS di Hong Kong, RPC)|1028 - Cinese (Taiwan)|  
    |5124 - Cinese (RAS di Macao)|1028 - Cinese (Taiwan)|  
    |1028 - Cinese (Taiwan)|Lingua predefinita|  
    |4100 - Cinese (Singapore)|2052 - Cinese (RPC)|  
    |2074 - Croato|Lingua predefinita|  
    |3098 - Croato (alfabeto cirillico)|Lingua predefinita|  
  
-   Per tutti gli altri identificatori di lingua specificati, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] estrae la lingua principale dell'identificatore specificato e recupera l'identificatore indicato da Windows come corrispondenza più appropriata per la lingua principale. Se non è possibile trovare una traduzione per l'identificatore di lingua che rappresenta la corrispondenza più appropriata o se l'identificatore specificato è la corrispondenza più appropriata per la lingua principale, viene utilizzata la lingua predefinita.  
  
## <a name="see-also"></a>Vedere anche  
 [Scenari di globalizzazione per Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Lingue e regole di confronto &#40;Analysis Services&#41;](../../analysis-services/languages-and-collations-analysis-services.md)  
  
  
