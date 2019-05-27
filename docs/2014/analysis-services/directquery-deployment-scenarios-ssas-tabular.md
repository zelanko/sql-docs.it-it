---
title: Scenari di distribuzione DirectQuery (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2aaf5cb8-294b-4031-94b3-fe605d7fc4c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a62a05c8908391b9ce925ecfe08ae30540b8fa29
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081644"
---
# <a name="directquery-deployment-scenarios-ssas-tabular"></a>Scenari di distribuzione DirectQuery (SSAS tabulare)
  In questo argomento viene fornita una procedura dettagliata del processo di progettazione e distribuzione per i modelli DirectQuery. È possibile configurare DirectQuery per l'utilizzo dei soli dati relazionali (solo DirectQuery) oppure è possibile configurare il modello per alternare l'utilizzo dei soli dati memorizzati nella cache o dei soli dati relazionali (modalità ibrida). In questo argomento viene illustrato il processo di implementazione per entrambe le modalità e vengono descritte le possibili differenze nei risultati della query a seconda della modalità e della configurazione della sicurezza.  
  
 [Progettazione e procedure di distribuzione](#bkmk_DQProcedure)  
  
 [Confronto di configurazioni di DirectQuery](#bkmk_Configurations)  
  
##  <a name="bkmk_DQProcedure"></a> Progettazione e procedure di distribuzione  
 **Passaggio 1. Creare la soluzione**  
  
 Indipendentemente dalla modalità che verrà utilizzata, è necessario rivedere le informazioni che descrivono le limitazioni riguardo ai dati che è possibile utilizzare nei modelli DirectQuery. Ad esempio, tutti i dati utilizzati nel modello e i report devono provenire da un solo database di SQL Server. Per altre informazioni, vedere [Modalità DirectQuery &#40;SSAS tabulare&#41;](tabular-models/directquery-mode-ssas-tabular.md).  
  
 Inoltre, consultare le limitazioni relative alle misure e alle colonne calcolate e determinare se le formule che si intende utilizzare sono compatibili con la modalità DirectQuery. Potrebbe essere necessario rimuovere o modificare gli elementi seguenti:  
  
-   Le colonne calcolate non sono supportate.  
  
-   Non è possibile utilizzare i dati incollati dall'operazione di copia. Se si importa un modello PowerPivot per avviare la soluzione, assicurarsi di eliminare le tabelle collegate prima di importare la soluzione, poiché questi dati non possono essere eliminati e causeranno il blocco della convalida di DirectQuery.  
  
 **Passaggio 2. Abilitare la modalità DirectQuery in Progettazione modelli**  
  
 Per impostazione predefinita, la modalità DirectQuery è disabilitata. Pertanto, è necessario configurare l'ambiente di progettazione per supportare la modalità DirectQuery.  
  
 Fare doppio clic il **Model. bim** nodo in Esplora soluzioni e impostare la proprietà **la modalità DirectQuery**, a `On`.  
  
 È possibile attivare la modalità DirectQuery in qualsiasi momento. Tuttavia, per assicurarsi di non creare colonne o formule incompatibili con la modalità DirectQuery, è consigliabile abilitare da subito la modalità DirectQuery.  
  
 Inizialmente, anche i modelli DirectQuery sono sempre creati in memoria. La modalità di query predefinita per il database dell'area di lavoro viene inoltre impostata su **DirectQuery con In-Memory**. Questa modalità operativa ibrida consente di utilizzare la cache dei dati importati per migliorare le prestazioni durante il processo di progettazione del modello, convalidando al contempo il modello rispetto ai requisiti di DirectQuery.  
  
 **Passaggio 3. Risolvere gli errori di convalida**  
  
 Se si verificano errori di convalida quando si attiva DirectQuery o si aggiungono nuovi dati o nuove formule, aprire l' **Elenco errori**di Visual Studio ed effettuare le azioni necessarie.  
  
-   Modificare le impostazioni delle proprietà necessarie per la modalità DirectQuery seguendo le indicazioni dei messaggi di errore.  
  
-   Rimuovere le colonne calcolate. Se è necessaria una colonna calcolata per una misura specifica, è sempre possibile creare la colonna utilizzando il [progettazione Query relazionale &#40;SSAS&#41; ](relational-query-designer-ssas.md) forniti nell'Importazione guidata tabella.  
  
-   Modificare o rimuovere le formule incompatibili con la modalità DirectQuery. Se un calcolo richiede una funzione particolare, valutare il modo in cui fornire un equivalente utilizzando Transact-SQL.  
  
-   Aggiungere i dati necessari.  Se nel modello sono stati utilizzati in precedenza dati da un'operazione copia-incolla o da provider diversi da SQL Server, è possibile creare nuove viste e nuove colonne derivate all'interno della connessione esistente o utilizzare query distribuite.  Tutti i dati utilizzati in un modello DirectQuery devono essere accessibili tramite una singola origine dati SQL Server.  
  
 **Passaggio 4. Impostare il metodo preferito per rispondere alle query sul modello**  
  
|||  
|-|-|  
|**Solo DirectQuery**|Impostare la proprietà su **DirectQuery**.|  
|**Modalità ibrida**|Impostare la proprietà su **In-Memory con DirectQuery** o **DirectQuery con In-Memory**.<br /><br /> È possibile modificare questo valore in un secondo momento per utilizzare una preferenza diversa.<br /><br /> Si noti che i client possono eseguire l'override del metodo preferito nella stringa di connessione.|  
  
 **Passaggio 5. Specificare la partizione DirectQuery**  
  
|||  
|-|-|  
|**Solo DirectQuery**|Facoltativo. Per un modello di tipo solo DirectQuery non occorre una partizione.<br /><br /> Tuttavia, se sono state create partizioni nel modello durante la fase di progettazione, solo una partizione può essere utilizzata come origine dati. Per impostazione predefinita, la prima partizione creata verrà utilizzata come partizione DirectQuery.<br /><br /> Per assicurarsi che tutti i dati richiesti dal modello siano disponibili nella partizione DirectQuery, scegliere una partizione DirectQuery e modificare l'istruzione SQL per ottenere l'intero set di dati.|  
|**Modalità ibrida**|Se una tabella nel modello dispone di più partizioni, è necessario scegliere una sola partizione come *partizione DirectQuery*. Se non si assegna una partizione, per impostazione predefinita la prima partizione creata verrà utilizzata come partizione DirectQuery.<br /><br /> Impostare le opzioni di elaborazione su tutte le partizioni tranne DirectQuery In genere, la partizione DirectQuery non viene mai elaborata perché i dati vengono passati dall'origine relazionale.<br /><br /> Per altre informazioni, vedere [partizioni e modalità DirectQuery &#40;modello tabulare di SSAS&#41;](tabular-models/define-partitions-in-directquery-models-ssas-tabular.md).|  
  
 **Passaggio 6. Configurare la rappresentazione**  
  
 La rappresentazione è supportata unicamente per i modelli DirectQuery. L'opzione di rappresentazione, **Impostazioni di rappresentazione**, consente di definire le credenziali utilizzate per la visualizzazione dei dati dall'origine dati SQL Server specificata.  
  
|||  
|-|-|  
|**Solo DirectQuery**|Per la proprietà  **Impostazioni di rappresentazione** , specificare l'account che verrà utilizzato per la connessione all'origine dati SQL Server.<br /><br /> Se si utilizza il valore **ImpersonateCurrentUser**, l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che ospita il modello passerà le credenziali dell'utente corrente del modello al database di SQL Server.|  
|**Modalità ibrida**|Per la proprietà **Impostazioni di rappresentazione** , specificare l'account che verrà utilizzato per accedere ai dati nell'origine dati SQL Server.<br /><br /> Questa impostazione non influisce sulle credenziali utilizzate per elaborare la cache utilizzata dal modello.|  
  
 **Passaggio 7. Distribuire il modello**  
  
 Quando si è pronti per distribuire il modello, aprire il **Project** dal menu di Visual Studio e selezionare **proprietà**. Impostare la proprietà **QueryMode** su uno dei valori descritti nella tabella seguente:  
  
 Per altre informazioni, vedere [distribuire da SQL Server Data Tools &#40;modello tabulare di SSAS&#41;](tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md).  
  
|||  
|-|-|  
|**Solo DirectQuery**|**DirectQueryOnly**<br /><br /> Poiché è stata impostata la modalità Solo Direct Query, i metadati del modello vengono distribuiti nel server, ma il modello non viene elaborato.<br /><br /> Si noti che la cache utilizzata dal database dell'area di lavoro non viene eliminata automaticamente. Per assicurarsi che gli utenti non possano visualizzare i dati memorizzati nella cache, cancellare il contenuto della cache in fase di progettazione. Per altre informazioni, vedere [Clear the Analysis Services Caches](instances/clear-the-analysis-services-caches.md).|  
|**Modalità ibrida**|**DirectQuery con In-Memory**<br /><br /> **In-Memory con DirectQuery**<br /><br /> Entrambi questi valori consentono di utilizzare la cache o l'origine dati relazionale secondo necessità. L'ordine determina l'origine dati che verrà utilizzata per impostazione predefinita per rispondere alle query sul modello.<br /><br /> In una modalità ibrida, l'elaborazione della cache deve avvenire contemporaneamente alla distribuzione dei metadati del modello nel server.<br /><br /> Dopo la distribuzione sarà possibile modificare questa impostazione.|  
  
 **Passaggio 8. Verificare il modello distribuito**  
  
 In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]aprire l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in cui è stato distribuito il modello. Fare clic con il pulsante destro del mouse sul nome del database e scegliere **Proprietà**.  
  
-   La proprietà **DirectQueryMode**è stata impostata al momento di definire le proprietà di distribuzione.  
  
-   La proprietà **Impostazioni di rappresentazione origine dati**è stata impostata al momento di definire le opzioni di rappresentazione dell'utente. Per altre informazioni, vedere [Impostare opzioni di rappresentazione &#40;SSAS - Multidimensionale&#41;](multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
-   È possibile modificare queste proprietà in qualsiasi momento dopo la distribuzione del modello.  
  
##  <a name="bkmk_Configurations"></a> Confronto tra le opzioni di DirectQuery  
 **Solo DirectQuery**  
 Questa opzione è da preferire quando si desidera garantire una singola origine dati o quando la memoria non è in grado di contenere i dati a causa delle loro dimensioni troppo elevate. Se si utilizza un'origine dati relazionale di grandi dimensioni, in fase di progettazione è possibile creare il modello utilizzando un subset dei dati. Quando si distribuisce il modello in modalità Solo DirectQuery, è possibile modificare la definizione dell'origine dati per includere tutti i dati obbligatori.  
  
 Preferire questa opzione anche quando si desidera utilizzare la sicurezza fornita dall'origine dati relazionale per controllare l'accesso utente ai dati. Con i modelli tabulari memorizzati nella cache, è anche possibile utilizzare i ruoli di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per controllare l'accesso ai dati, tuttavia anche i dati archiviati nella cache devono essere protetti. Utilizzare sempre questa opzione se il contesto di sicurezza richiede che i dati non vengano mai memorizzati nella cache.  
  
 Nella tabella seguente vengono descritti i possibili risultati della distribuzione per la modalità Solo DirectQuery:  
  
|||  
|-|-|  
|**DirectQuery senza cache**|Non sono stati caricati dati nella cache. Il modello non potrà mai essere elaborato.<br /><br /> Sarà possibile eseguire query sul modello solo utilizzando client che supportano le query DAX. I risultati delle query vengono sempre restituiti dall'origine dati originale.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **DirectQuery**|  
|**DirectQuery con query solo sulla cache**|La distribuzione non viene eseguita. Questa configurazione non è supportata.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **In-Memory**|  
  
 **Modalità ibrida**  
 La distribuzione del modello in una modalità ibrida comporta molti vantaggi: la possibilità di ottenere dati aggiornati dall'origine dati SQL Server secondo necessità, ma conservando la cache, consente di lavorare con i dati in memoria e di ottenere prestazioni più elevate durante la progettazione di report o il test del modello.  
  
 Una modalità ibrida DirectQuery è inoltre utile se le dimensioni del modello sono grandi. Per evitare che gli utenti ottengano dati non aggiornati o che il modello non sia disponibile durante l'elaborazione della cache, è possibile impostare la modalità DirectQuery durante l'elaborazione. Anche se potrebbe verificarsi un leggero calo delle prestazioni, gli utenti sarebbero comunque in grado di ottenere i dati direttamente dall'archivio relazionale, con risultati aggiornati.  
  
 Nella tabella seguente viene confrontato il risultato della distribuzione in ognuna delle combinazioni di opzioni DirectQuery.  
  
|||  
|-|-|  
|**Modalità ibrida con cache preferita**|Il modello può essere elaborato e i dati possono essere caricati nella cache. Per impostazione predefinita, per le query viene utilizzata la cache.  Se un client desidera utilizzare l'origine DirectQuery, è necessario inserire un parametro nella stringa di connessione.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **In-Memory with DirectQuery**|  
|**Modalità ibrida con DirectQuery preferita**|Il modello viene elaborato e i dati possono essere caricati nella cache. Per impostazione predefinita, le query utilizzano tuttavia DirectQuery. Se un client desidera utilizzare i dati memorizzati nella cache, è necessario inserire un parametro nella stringa di connessione. Se le tabelle del modello sono partizionate, anche la partizione principale della cache viene impostata su **In-Memory con DirectQuery**.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **DirectQuery con In-Memory**|  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità DirectQuery &#40;SSAS tabulare&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [Accesso ai dati di modello tabulare](tabular-models/tabular-model-data-access.md)  
  
  
