---
title: Creare un progetto di Analysis Services (SSDT) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4fe65216ad293786496f412c9cc1451e6b92a7bf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866998"
---
# <a name="create-an-analysis-services-project-ssdt"></a>Creare un progetto di Analysis Services (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  È possibile definire un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando il modello di progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o l'Importazione guidata database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per leggere il contenuto di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]non è attualmente caricata alcuna soluzione, creando un nuovo progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene automaticamente creata una nuova soluzione. In caso contrario, il nuovo progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sarà aggiunto alla soluzione esistente. Le procedure consigliate per lo sviluppo di soluzioni prevedono la creazione di progetti separati per tipi diversi di dati dell'applicazione, utilizzando una sola soluzione se i progetti sono correlati. Ad esempio, potrebbe essere disponibile una sola soluzione contenente progetti separati per i pacchetti di Integration Services, i database di Analysis Services e i report di Reporting Services utilizzati dalla stessa applicazione aziendale.  
  
 In un progetto di Analysis Services sono contenuti gli oggetti utilizzati in un solo database di Analysis Services. Le proprietà di distribuzione del progetto consentono di specificare il nome del server e del database con cui i metadati del progetto verranno distribuiti come oggetti di cui è stata creata un'istanza.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Creare un nuovo progetto utilizzando il modello di progetto di Analysis Services](#bkmk_NewUsingTemplate)  
  
 [Creare un nuovo progetto utilizzando un database esistente di Analysis Services](#bkmk_NewUsingWizard)  
  
 [Aggiungere un progetto di Analysis Services in una soluzione esistente](#bkmk_AddtoExistingSolution)  
  
 [Compilare e distribuire la soluzione](#bkmk_buildDeploy)  
  
 [Cartelle del progetto di Analysis Services](#bkmk_ProjectFolders)  
  
 [Tipi di file di Analysis Services](#bkmk_FileTypes)  
  
 [Modelli di elementi di Analysis Services](#bkmk_ItemTemplates)  
  
##  <a name="bkmk_NewUsingTemplate"></a> Creare un nuovo progetto utilizzando il modello di progetto di Analysis Services  
 Usare queste istruzioni per creare un progetto vuoto in cui definire gli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , che possono quindi essere distribuiti come nuovo database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic su **File**, selezionare **Nuovo**e fare clic su **Progetto**. Nel riquadro **Tipi progetto** nella finestra di dialogo **Nuovo progetto** selezionare **Progetti Business Intelligence**.  
  
2.  Nella categoria **Modelli Visual Studio installati** nella finestra di dialogo **Nuovo progetto** selezionare **Progetto di Analysis Services**.  
  
3.  Nella casella di testo **Nome** digitare il nome del progetto. Il nome immesso sarà utilizzato come nome del database predefinito.  
  
4.  Nell'elenco a discesa **Percorso** digitare o selezionare la cartella in cui archiviare i file del progetto oppure fare clic su **Sfoglia** per selezionare una cartella.  
  
5.  Per aggiungere il nuovo progetto alla soluzione esistente, nell'elenco a discesa **Soluzione** selezionare **Aggiungi a soluzione**.  
  
     oppure  
  
     Per creare una nuova soluzione, nell'elenco a discesa **Soluzione** selezionare **Crea nuova soluzione**. Per creare una nuova cartella per la nuova soluzione, selezionare **Crea directory per soluzione**. In **Nome soluzione**digitare il nome della nuova soluzione.  
  
6.  Fare clic su **OK**.  
  
##  <a name="bkmk_NewUsingWizard"></a> Creare un nuovo progetto utilizzando un database esistente di Analysis Services  
 Usare l'Importazione guidata database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per creare un progetto basato sugli oggetti del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente. In caso di definizione di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] basato su un database esistente di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , i metadati di tale database verranno aperti in un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Questi oggetti possono essere quindi modificati all'interno del progetto, senza impatto sugli oggetti originali, e successivamente essere distribuiti nello stesso database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , se le proprietà di distribuzione specificano il database, oppure in un nuovo database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] creato per test di confronto. Finché le modifiche non vengono distribuite, nessuna ha impatto sul database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente.  
  
 È inoltre possibile utilizzare il modello Importa database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per creare un progetto da un database di produzione al quale sono state apportate direttamente modifiche in seguito alla distribuzione del progetto originale di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Prima di elaborare o distribuire il progetto, potrebbe essere necessario modificare il provider di dati specificato nelle origini dati. Se il software SQL Server in uso è più recente del software utilizzato per creare il database, il provider di dati specificato nel progetto potrebbe non essere installato nel computer. Durante l'elaborazione, l'account del servizio sarà utilizzato per recuperare i dati nel database di Analysis Services. Se il database si trova in un server remoto, controllare se il servizio locale dispone di autorizzazioni di elaborazione e di lettura in tale server.  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic su **File**, selezionare **Nuovo**e fare clic su **Progetto**. Nel riquadro **Tipi progetto** nella finestra di dialogo **Nuovo progetto** selezionare **Progetti Business Intelligence**.  
  
2.  Nella categoria **Modelli Visual Studio installati** nella finestra di dialogo **Nuovo progetto** selezionare **Importa database di Analysis Services**.  
  
3.  Immettere le informazioni sulle proprietà per il progetto e la soluzione, inclusi il nome e il percorso dei file. Fare clic su **OK**.  
  
4.  Nella pagina **Importazione guidata database di Analysis Services** fare clic su **Avanti**.  
  
5.  Nella pagina **Database di origine** specificare il server e il database da cui la procedura guidata estrarrà il contenuto e creerà il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e quindi fare clic su **Avanti**.  
  
     Tra i database supportati sono inclusi quelli creati nelle versioni seguenti di Analysis Services: [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
     È possibile digitare il nome del database oppure eseguire una query sul server per visualizzare i database esistenti in tale server. Se il database si trova in un server remoto o in un server di produzione, potrebbe essere necessario richiedere l'autorizzazione per leggere il database. Le impostazioni di configurazione del firewall possono ulteriormente limitare l'accesso a un database. Se viene visualizzato un errore durante il tentativo di connettersi al database, controllare innanzitutto le autorizzazioni e le impostazioni del firewall.  
  
6.  Quando la procedura guidata completa l'estrazione del contenuto del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , fare clic su **Fine** nella pagina **Completamento procedura guidata** .  
  
7.  Aprire la finestra Esplora soluzioni per visualizzare il contenuto del progetto.  
  
##  <a name="bkmk_AddtoExistingSolution"></a> Aggiungere un progetto di Analysis Services in una soluzione esistente  
 Se si dispone già di una soluzione contenente tutti i file di origine di un'applicazione aziendale, è possibile aggiungervi un nuovo progetto di Analysis Services.  
  
 L'aggiunta di un progetto esistente a una soluzione consente di associare il progetto alla soluzione, ma non di copiarlo. Se il progetto di Analysis Services è stato creato in una soluzione diversa, i file del progetto rimangono nella soluzione originale per cui è stato creato. Pertanto, tutte le modifiche apportate al progetto tramite entrambe le soluzioni verranno applicate allo stesso set di file di origine. Se questo non è il comportamento previsto, è consigliabile innanzitutto copiare o spostare i file del progetto nella cartella della nuova soluzione, quindi aggiungere il progetto alla soluzione.  
  
1.  Aprire la soluzione in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. In Esplora soluzioni fare clic con il pulsante destro del mouse sulla soluzione, scegliere **Aggiungi**e quindi fare clic su **Progetto esistente** per selezionare il progetto che si vuole aggiungere.  
  
2.  Selezionare un file con estensione dwproj per aggiungerlo alla soluzione.  
  
##  <a name="bkmk_buildDeploy"></a> Compilare e distribuire la soluzione  
 Per impostazione predefinita, il progetto viene distribuito da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nell'istanza predefinita di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sul computer locale. È possibile modificare la destinazione di distribuzione usando la finestra di dialogo **Pagine delle proprietà** per il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per modificare la proprietà di configurazione **Server** .  
  
> [!NOTE]  
>  Per impostazione predefinita, durante la distribuzione di una soluzione vengono elaborati in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] soltanto gli oggetti modificati dallo script di distribuzione e gli oggetti dipendenti. È possibile modificare questa funzionalità usando la finestra di dialogo **Pagine delle proprietà** del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per modificare la proprietà di configurazione Opzione di elaborazione.  
  
 Compilare e distribuire la soluzione in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per eseguirne il test. Con la compilazione di una soluzione vengono convalidate le definizioni e le dipendenze degli oggetti nel progetto e viene generato uno script di distribuzione. Durante la distribuzione di una soluzione viene utilizzato il motore di distribuzione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per l'invio dello script di distribuzione a un'istanza specificata.  
  
 Dopo aver distribuito il progetto, controllare e testare il database distribuito. Successivamente, è possibile modificare le definizioni dell'oggetto, eseguire la compilazione e nuovamente la distribuzione finché il progetto non viene completato.  
  
 Dopo aver completato il progetto, è possibile utilizzare la Distribuzione guidata per distribuire lo script di distribuzione, generato durante la compilazione della soluzione, nelle istanze di destinazione a scopo di test finale, gestione temporanea e distribuzione.  
  
##  <a name="bkmk_ProjectFolders"></a> Cartelle del progetto di Analysis Services  
 Un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contiene le cartelle seguenti, usate per organizzare gli elementi inclusi nel progetto.  
  
|Cartella|Descrizione|  
|------------|-----------------|  
|Origini dati|Contiene le origini dati di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questi oggetti vengono creati tramite la Creazione guidata origine dati e modificati in Progettazione origine dati.|  
|Viste origine dati|Contiene le viste origine dati di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questi oggetti vengono creati tramite la Creazione guidata vista origine dati e modificati in Progettazione vista origine dati.|  
|Cubi|Contiene i cubi di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questi oggetti vengono creati tramite la Creazione guidata cubo e modificati in Progettazione cubi.|  
|Dimensioni|Contiene le dimensioni di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questi oggetti vengono creati tramite la Creazione guidata dimensione o la Creazione guidata cubo e modificati in Progettazione dimensioni.|  
|Strutture di data mining|Contiene le strutture di data mining di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questi oggetti vengono creati tramite la Creazione guidata modello di data mining e modificati in Progettazione modelli di data mining.|  
|Ruoli|Contiene i ruoli del database di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . I ruoli vengono creati e gestiti in Progettazione ruoli.|  
|Assembly|Contiene i riferimenti a librerie COM e assembly [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . I riferimenti vengono creati nella finestra di dialogo **Aggiungi riferimento** .|  
|Varie|Contiene qualsiasi tipo di file, tranne i file di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Utilizzare questa cartella per aggiungere eventuali file esterni, ad esempio file di testo contenenti note sul progetto.|  
  
##  <a name="bkmk_FileTypes"></a> Tipi di file di Analysis Services  
 In una soluzione di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] possono essere inclusi vari tipi di file a seconda dei progetti compresi nella soluzione e degli elementi di ogni progetto della soluzione. In genere i file per ogni progetto in una soluzione di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sono archiviati nella cartella della soluzione, una separata per ogni progetto.  
  
> [!NOTE]  
>  Quando si copia un file di oggetto in una cartella del progetto, l'oggetto non viene aggiunto al progetto. Per aggiungere una definizione di oggetto esistente a un progetto, è necessario usare il comando **Aggiungi** del menu contestuale del progetto in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
 La cartella di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può contenere i tipi di file elencati nella tabella seguente.  
  
|Tipo di file|Descrizione|  
|---------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] File di destinazione del progetto (estensione dwproj)|Contiene i metadati relativi a elementi, configurazioni e riferimenti ad assembly definiti e inclusi nel progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Impostazioni utente del progetto (estensione dwproj.user)|Contiene le informazioni di configurazione del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per un utente specifico.|  
|File di origine dei dati (ds)|Contiene gli elementi [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language (ASSL) che definiscono i metadati di un'origine dati.|  
|File di vista origine dati (dsv)|Contiene gli elementi ASSL che definiscono i metadati di una vista origine dati.|  
|File di cubo (cube)|Contiene gli elementi ASSL che definiscono i metadati di un cubo, inclusi i gruppi di misure, le misure e le dimensioni del cubo.|  
|File di partizione (partitions)|Contiene gli elementi ASSL che definiscono i metadati delle partizioni del cubo specificato.|  
|File di dimensione (dim)|Contiene gli elementi ASSL che definiscono i metadati di una dimensione del database.|  
|File di struttura di data mining (dmm)|Contiene gli elementi ASSL che definiscono i metadati di una struttura di data mining e i modelli di data mining associati.|  
|File di database (database)|Contiene gli elementi ASSL che definiscono i metadati di un database, compresi i tipi di conto, le traduzioni e le autorizzazioni del database.|  
|File di ruolo del database (role)|Contiene gli elementi ASSL che consentono di definire i metadati di un ruolo del database, compresi i membri del ruolo.|  
  
##  <a name="bkmk_ItemTemplates"></a> Modelli di elementi di Analysis Services  
 Se si usa la finestra di dialogo **Aggiungi nuovo elemento** per aggiungere nuovi elementi a un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è possibile scegliere di usare un modello di elemento, uno script predefinito o un'istruzione che mostra come seguire un'azione specificata.  
  
 I modelli di elemento, elencati nella tabella seguente, sono disponibili nella categoria Elementi progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , visualizzata nella finestra di dialogo **Aggiungi nuovo elemento** .  
  
|Category|Modello di elementi|Descrizione|  
|--------------|-------------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Elementi del progetto|Cube|Avvia la Creazione guidata cubo per l'aggiunta di un nuovo cubo al progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||origine dati|Avvia la Creazione guidata origine dati per l'aggiunta di una nuova origine dati al progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||Vista origine dati|Avvia la Creazione guidata vista origine dati per l'aggiunta di una nuova vista origine dati al progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||Ruolo del database|Aggiunge un nuovo ruolo di database al progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e determina quindi la visualizzazione di Progettazione ruoli per il nuovo ruolo.|  
||Dimension|Avvia la Creazione guidata dimensione per l'aggiunta di una nuova dimensione del database al progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||Struttura di data mining|Avvia la Creazione guidata modello di data mining per l'aggiunta di una nuova struttura di data mining e del modello di data mining associato al progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare proprietà di progetti di Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)   
 [Compilare progetti di Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [Distribuire progetti di Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
