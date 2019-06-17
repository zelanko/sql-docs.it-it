---
title: Variabili di Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- user-defined variables [Integration Services]
- scope [Integration Services]
- system variables [Integration Services]
- variables [Integration Services]
- variables [Integration Services], about variables
- values [Integration Services]
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5f286a0cd957ed62ab3edb51eb96565431afb22a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65723532"
---
# <a name="integration-services-ssis-variables"></a>Variabili di Integration Services (SSIS)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Nelle variabili vengono archiviati valori che possono essere usati in fase di esecuzione da un pacchetto di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e dai relativi contenitori, attività e gestori di eventi. Anche gli script nell'attività Script e nel componente script possono utilizzare le variabili. I vincoli di precedenza che definiscono la sequenza delle attività e dei contenitori in un flusso di lavoro possono utilizzare variabili quando le definizioni di vincolo includono espressioni.  
  
 Nei pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è possibile usare variabili per gli scopi seguenti:  
  
-   Aggiornamento delle proprietà degli elementi dei pacchetti in fase di esecuzione. È ad esempio possibile impostare dinamicamente il numero di eseguibili simultanei consentiti in un contenitore Ciclo Foreach.  
  
-   Inclusione di una tabella di ricerca in memoria. Un pacchetto può ad esempio eseguire un'attività Esegui SQL che carica una variabile con valori di dati.  
  
-   Caricamento di variabili con valori di dati da utilizzare per specificare una condizione di ricerca in una clausola WHERE. Lo script in un'attività Script può ad esempio aggiornare il valore di una variabile utilizzata da un'istruzione Transact-SQL in un'attività Esegui SQL.  
  
-   Caricamento di una variabile con un valore intero da utilizzare per il controllo del ciclo in un flusso di controllo di un pacchetto. È ad esempio possibile utilizzare una variabile nell'espressione di valutazione di un contenitore Ciclo For per controllare l'iterazione.  
  
-   Popolamento di valori di parametri per istruzioni Transact-SQL in fase di esecuzione. Un pacchetto può ad esempio eseguire un'attività Esegui SQL e quindi utilizzare variabili per impostare dinamicamente i parametri in un'istruzione Transact-SQL.  
  
-   Compilazione di espressioni che includono valori di variabili. La trasformazione Colonna derivata può ad esempio popolare una colonna con i risultati ottenuti moltiplicando il valore di una variabile per il valore di una colonna.  
  
## <a name="system-and-user-defined-variables"></a>Variabili definite dall'utente e variabili di sistema  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] supporta due tipi di variabili: variabili definite dall'utente e variabili di sistema. Le variabili definite dall'utente vengono definite dagli sviluppatori dei pacchetti, mentre quelle di sistema sono definite da [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. È possibile creare un numero illimitato di variabili definite dall'utente, ma non è possibile creare ulteriori variabili di sistema.  
  
 Tutte le variabili, sia di sistema che definite dall'utente, possono essere usate nelle associazioni di parametro con cui l'attività Esegui SQL esegue il mapping delle variabili ai parametri nelle istruzioni SQL. Per altre informazioni, vedere [Attività Esegui SQL](../integration-services/control-flow/execute-sql-task.md) e [Parametri e codici restituiti nell'attività Esegui SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).  
  
> [!NOTE]  
>  Per i nomi delle variabili di sistema e delle variabili definite dall'utente viene fatta distinzione tra maiuscole e minuscole.  
  
 È possibile creare variabili definite dall'utente per tutti i tipi di contenitori di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , ovvero pacchetti, contenitori Ciclo Foreach, contenitori Ciclo For, contenitori Sequenza, attività e gestori di eventi. Le variabili definite dall'utente sono membri della raccolta Variables del contenitore.  
  
 Se si crea il pacchetto usando Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] , sarà possibile vedere i membri di una raccolta Variables nella cartella **Variabili** della scheda **Esplora pacchetti** di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] . Nelle cartelle vengono elencate sia le variabili definite dall'utente che le variabili di sistema.  
  
 Nella configurazione delle variabili definite dall'utente è possibile:  
  
-   Specificare un nome e una descrizione per la variabile.  
  
-   Specificare uno spazio dei nomi per la variabile.  
  
-   Indicare se la variabile genera un evento quando il relativo valore viene modificato.  
  
-   Indicare se la variabile è in sola lettura o in lettura e scrittura.  
  
-   Utilizzare il risultato della valutazione di un'espressione per impostare il valore della variabile.  
  
-   Creare la variabile nell'ambito del pacchetto o di un oggetto del pacchetto, ad esempio un'attività.  
  
-   Specificare il valore e il tipo di dati della variabile.  
  
 L'unica opzione configurabile delle variabili di sistema è quella che determina se debba essere generato o meno un evento quando il valore viene modificato.  
  
 Per ogni tipo di contenitore è disponibile un set di variabili di sistema specifico. Per altre informazioni sulle variabili di sistema usate dai pacchetti e dai relativi elementi, vedere [Variabili di sistema](../integration-services/system-variables.md).  
  
 Per altre informazioni su scenari reali relativi all'uso delle variabili, vedere [Utilizzo di variabili nei pacchetti](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="properties-of-variables"></a>Proprietà delle variabili  
 È possibile configurare le variabili definite dall'utente impostando le proprietà seguenti nella finestra **Variabili** o nella finestra **Proprietà** . Alcune proprietà sono disponibili solo nella finestra Proprietà.  
  
> [!NOTE]  
>  L'unica opzione configurabile delle variabili di sistema è quella che determina se debba essere generato o meno un evento quando il valore viene modificato.  
  
 **Description**    
 Specifica la descrizione della variabile.  
  
 **EvaluateAsExpression**    
 Quando la proprietà è impostata su **True**, viene usata l'espressione fornita per impostare il valore della variabile.  
  
 **Espressione**    
 Specifica l'espressione assegnata alla variabile.  
  
 **Nome**    
 Specifica il nome della variabile.  
  
 **Spazio dei nomi**  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] offre due spazi dei nomi: **User** e **System**. Per impostazione predefinita, le variabili personalizzate appartengono allo spazio dei nomi **User** , mentre le variabili di sistema appartengono allo spazio dei nomi **System** . È possibile creare altri spazi dei nomi per le variabili definite dall'utente e modificare il nome dello spazio dei nomi **User** , ma non è possibile modificare il nome dello spazio dei nomi **System** , né aggiungere variabili allo spazio dei nomi **System** o assegnare variabili di sistema a uno spazio dei nomi diverso.  
  
**RaiseChangedEvent**  
 Se la proprietà è impostata su **True**, quando viene modificato il valore della variabile viene generato l'evento **OnVariableValueChanged** .  
  
 **ReadOnly**  
 Quando la proprietà è impostata su **False**, la variabile è in lettura/scrittura.  
  
**Ambito**    
 > [!NOTE]  
>  È possibile modificare questa proprietà solo facendo clic su **Sposta variabile** nella finestra **Variabili** .  
  
 Le variabili vengono create nell'ambito di un pacchetto o nell'ambito di un contenitore, attività o gestore di evento di un pacchetto. Poiché il contenitore del pacchetto costituisce il livello principale della gerarchia dei contenitori, le variabili con ambito pacchetto sono variabili globali e possono essere utilizzate da tutti i contenitori del pacchetto. Analogamente, le variabili definite nell'ambito di un contenitore, quale Ciclo For, possono essere utilizzate da tutti i contenitori e le attività inclusi nel contenitore Ciclo For.  
  
 Se un pacchetto esegue altri pacchetti utilizzando l'attività Esegui pacchetto, sarà possibile utilizzare il tipo di configurazione Variabile pacchetto padre per rendere disponibili al pacchetto chiamato le variabili definite nell'ambito del pacchetto chiamante o dell'attività Esegui pacchetto. Per altre informazioni, vedere [Configurazioni di pacchetto](../integration-services/packages/package-configurations.md).  
  
**IncludeInDebugDump**  
 Indica se il valore della variabile viene incluso nei file di dump del debug.  
  
 Per variabili definite dall'utente e variabili di sistema, il valore predefinito per l'opzione **InclueInDebugDump** è **true**.  
  
 Per le variabili definite dall'utente, tuttavia, l'opzione **IncludeInDebugDump** viene reimpostata su **false** quando sono rispettate le condizioni seguenti:  
  
-   Se la proprietà della variabile **EvaluateAsExpression** è impostata su **true**, l'opzione **IncludeInDebugDump** verrà reimpostata su **false**.  
  
     Per includere il testo dell'espressione come valore della variabile nei file di dump del debug, impostare l'opzione **IncludeInDebugDump** su **true**.  
  
-   Se il tipo di dati della variabile viene cambiato in String, l'opzione **IncludeInDebugDump** verrà reimpostata su **false**.  
  
 Durante la reimpostazione dell'opzione **IncludeInDebugDump** su **false**può essere eseguito l'override del valore selezionato dall'utente.  
  
**Valore**    
Il valore di una variabile definita dall'utente può essere un valore letterale o un'espressione. Il valore di una variabile non può essere null. Le variabili hanno i seguenti valori predefiniti:

| Tipo di dati | Valore predefinito |
|---|---|
| Boolean | False |
| Tipi di dati numerici e binari | 0 (zero) |
| Tipi di dati char e stringa | (stringa vuota) |
| Object | System.Object |
| | |

Le variabili includono opzioni per l'impostazione del valore della variabile e del relativo tipo di dati. Queste due proprietà devono essere compatibili. Non è ad esempio possibile utilizzare un valore stringa insieme a un tipo di dati Integer.  
  
 Se la variabile è configurata in modo da essere valutata come espressione, sarà necessario specificare un'espressione. In fase di esecuzione l'espressione verrà valutata e la variabile verrà impostata sul risultato della valutazione. Se ad esempio una variabile usa l'espressione `DATEPART("month", GETDATE())` , assumerà un valore equivalente al numero del mese della data corrente. È necessario utilizzare un'espressione valida che utilizza la sintassi della grammatica delle espressioni di [!INCLUDE[ssIS](../includes/ssis-md.md)] . Quando si utilizza un'espressione con variabili, quest'ultima può includere valori letterali, nonché le funzioni e gli operatori previsti dalla grammatica delle espressioni, ma non può fare riferimento a colonne di un flusso di dati del pacchetto. Un'espressione può avere una lunghezza massima di 4000 caratteri. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
**ValueType**    
 > [!NOTE]  
>  Il valore della proprietà viene visualizzato nella colonna **Tipo di dati** della finestra **Variabili** .  
  
 Specificare il tipo di dati del valore della variabile.  

## <a name="scenarios-for-using-variables"></a>Scenari di utilizzo delle variabili  
 Nei pacchetti [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] le variabili vengono utilizzate in diversi modi. Durante lo sviluppo di un pacchetto vengono in genere aggiunte variabili definite dall'utente allo scopo di implementare la flessibilità e la gestibilità richieste dalla soluzione. A seconda dello scenario, vengono comunemente utilizzate anche variabili di sistema.  
  
 **Espressioni di proprietà** Usano le variabili per specificare i valori nelle espressioni di proprietà che impostano gli oggetti e le proprietà dei pacchetti. L'espressione `SELECT * FROM @varTableName` , ad esempio, include la variabile `varTableName` che aggiorna l'istruzione SQL eseguita da un'attività Esegui SQL. L'espressione `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`" aggiorna il pacchetto eseguito dall'attività Esegui pacchetto, eseguendo il pacchetto specificato nella variabile `varPackageFirst` il primo giorno del mese e il pacchetto specificato nella variabile `varPackageOther` in altri giorni. Per altre informazioni, vedere [Utilizzo delle espressioni di proprietà nei pacchetti](../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 **Espressioni del flusso di dati** Usano le variabili per specificare valori nelle espressioni usate dalle trasformazioni Colonna derivata e Suddivisione condizionale per popolare le colonne o per indirizzare le righe di dati nell'output di altre trasformazioni. L'espressione `@varSalutation + LastName`, ad esempio, concatena il valore della variabile `VarSalutation` e della colonna `LastName` . L'espressione `Income < @HighIncome` indirizza in un output le righe di dati in cui il valore della colonna `Income` è minore del valore della variabile `HighIncome`. Per altre informazioni, vedere [Trasformazione Colonna derivata](../integration-services/data-flow/transformations/derived-column-transformation.md), [Trasformazione Suddivisione condizionale](../integration-services/data-flow/transformations/conditional-split-transformation.md), e [Espressioni di Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 **Espressioni di vincoli di precedenza** Forniscono i valori da usare nei vincoli di precedenza per determinare se l'eseguibile soggetto al vincolo verrà eseguito o meno. Le espressioni possono essere utilizzate insieme al risultato di un'esecuzione (esito positivo, esito negativo, completamento) o in sostituzione di tale risultato. Se ad esempio l'espressione `@varMax > @varMin`restituisce **true**, l'eseguibile verrà eseguito. Per altre informazioni, vedere [Aggiunta di espressioni ai vincoli di precedenza](https://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1).  
  
 **Parametri e codici restituiti** Forniscono i valori ai parametri di input o archiviano i valori dei parametri di output e i codici restituiti. A tale scopo viene eseguito il mapping delle variabili ai parametri e ai valori restituiti. Se ad esempio si imposta la variabile `varProductId` su 23 e si esegue l'istruzione SQL `SELECT * from Production.Product WHERE ProductID = ?`, la query recupera il prodotto il cui `ProductID` ha valore 23. Per altre informazioni, vedere [Attività Esegui SQL](../integration-services/control-flow/execute-sql-task.md) e [Parametri e codici restituiti nell'attività Esegui SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).  
  
 **Espressioni del Ciclo For** Forniscono i valori da usare nell'inizializzazione, la valutazione e l'assegnazione di espressioni del Ciclo For. Se ad esempio la variabile `varCount` è uguale a 2 e `varMaxCount` è uguale a 10, l'espressione di inizializzazione è `@varCount`, quella di valutazione è  `@varCount < @varMaxCount`e quella di assegnazione è `@varCount =@varCount +1`, pertanto il ciclo si ripete 8 volte. Per altre informazioni, vedere [Contenitore Ciclo For](../integration-services/control-flow/for-loop-container.md).  
  
 **Configurazioni Variabile pacchetto padre** Passano i valori dai pacchetti padre ai pacchetti figlio. Queste configurazioni consentono ai pacchetti figlio di accedere alle variabili del pacchetto padre. Se ad esempio il pacchetto figlio deve utilizzare la stessa data del pacchetto padre, sarà possibile definire un tipo di configurazione Variabile pacchetto padre che specifichi un set di variabili tramite la funzione GETDATE nel pacchetto padre. Per altre informazioni, vedere [Attività Esegui pacchetto](../integration-services/control-flow/execute-package-task.md) e [Configurazioni di pacchetto](../integration-services/packages/package-configurations.md).  
  
 **Attività Script e componente script** Forniscono un elenco di variabili di sola lettura e di lettura/scrittura all'attività Script o al componente script, aggiornano le variabili di lettura/scrittura all'interno dello script, quindi usano i valori aggiornati all'interno o all'esterno dello script. Ad esempio, nel codice `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`la variabile di script `numberOfCars` viene aggiornata dal valore della variabile `NumberOfCars`. Per altre informazioni, vedere [Utilizzo di variabili nell'attività Script](../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md).  

## <a name="add-a-variable"></a>Aggiungere una variabile  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che si desidera utilizzare.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] eseguire una delle operazioni seguenti per definire l'ambito della variabile:  
  
    -   Per impostare il pacchetto come ambito, fare clic in un punto qualsiasi dell'area di progettazione della scheda **Flusso di controllo** .  
  
    -   Per impostare un gestore dell'evento come ambito, selezionare un file eseguibile e un gestore dell'evento nell'area di progettazione della scheda **Gestore evento** .  
  
    -   Per impostare un'attività o un contenitore come ambito, nell'area di progettazione della scheda **Flusso di controllo** o **Gestore evento** fare clic su un'attività o un contenitore.  
  
4.  Scegliere **Variabili** dal menu **SSIS**. Facoltativamente, è possibile visualizzare la finestra **Variabili** eseguendo il mapping del comando View.Variables a una combinazione di tasti scelta dall'utente nella pagina **Tastiera** della finestra di dialogo **Opzioni** .  
  
5.  Nella finestra **Variabili** fare clic sull'icona **Aggiungi variabile** . La nuova variabile verrà aggiunta all'elenco.  
  
6.  Facoltativamente, fare clic sull'icona **Opzioni griglia** , selezionare le colonne aggiuntive da visualizzare nella finestra di dialogo **Variables Grid Options** (Opzioni griglia variabili) e quindi fare clic su **OK**.  
  
7.  Facoltativamente, impostare le proprietà delle variabili. Per altre informazioni, vedere [Impostazione delle proprietà di una variabile definita dall'utente](https://msdn.microsoft.com/library/f98ddbec-f668-4dba-a768-44ac3ae0536f).  
  
8.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  

### <a name="add-variable-dialog-box"></a>Aggiungi variabile - finestra di dialogo
Usare la finestra di dialogo **Aggiungi variabile** per specificare le proprietà di una nuova variabile.  
  
#### <a name="options"></a>Opzioni  
 **Contenitore**  
 Selezionare un contenitore nell'elenco. Il contenitore definisce l'ambito della variabile e può essere un pacchetto o un file eseguibile nel pacchetto.  
  
 **Nome**  
 Consente di digitare il nome della variabile.  
  
 **Namespace**  
 Consente di specificare lo spazio dei nomi della variabile. Per impostazione predefinita, le variabili definite dall'utente si trovano nello spazio dei nomi **Utente** .  
  
 **Tipo valore**  
 Consente di selezionare un tipo di dati.  
  
 **Value**  
 Consente di digitare un valore. Il valore deve essere compatibile con il tipo di dati specificato nell'opzione **Tipo valore** .  
  
 **Sola lettura**  
 Selezionare questa opzione se il valore deve essere di sola lettura.  
   
## <a name="delete-a-variable"></a>Eliminare una variabile  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul pacchetto in modo da aprirlo.  
  
3.  Scegliere **Variabili** dal menu **SSIS**. Facoltativamente, è possibile visualizzare la finestra **Variabili** eseguendo il mapping del comando View.Variables a una combinazione di tasti scelta dall'utente nella pagina **Tastiera** della finestra di dialogo **Opzioni** .  
  
4.  Selezionare la variabile che si desidera eliminare e quindi fare clic su **Elimina variabile**.  
  
     Se la variabile non viene visualizzata nella finestra Variabili, fare clic su **Opzioni griglia** e quindi selezionare **Mostra variabili di tutti gli ambiti**.  
  
5.  Se viene visualizzata la finestra di dialogo **Conferma eliminazione variabili** , fare clic su **Sì** per confermare.  
  
6.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="change-the-scope-of-a-variable"></a>Modificare l'ambito di una variabile  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul pacchetto in modo da aprirlo.  
  
3.  Scegliere **Variabili** dal menu **SSIS**. Facoltativamente, è possibile visualizzare la finestra **Variabili** eseguendo il mapping del comando View.Variables a una combinazione di tasti scelta dall'utente nella pagina **Tastiera** della finestra di dialogo **Opzioni** .  
  
4.  Selezionare la variabile e quindi fare clic su **Sposta variabile**.  
  
     Se la variabile non viene visualizzata nella finestra Variabili, fare clic su **Opzioni griglia** e quindi selezionare **Mostra variabili di tutti gli ambiti**.  
  
5.  Nella finestra di dialogo **Seleziona nuovo ambito** selezionare il pacchetto oppure un contenitore, un'attività o un gestore eventi del pacchetto per modificare l'ambito della variabile.  
  
6.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  

## <a name="set-the-properties-of-a-user-defined-variable"></a>Impostazione delle proprietà di una variabile definita dall'utente
 Per impostare le proprietà di una variabile definita dall'utente in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]è possibile utilizzare una delle funzionalità seguenti:  
  
-   Finestra Variabili.  
  
-   Finestra Proprietà. Nella finestra **Proprietà** sono elencate le proprietà per la configurazione delle variabili non disponibili nella finestra **Variabili**: Description, EvaluateAsExpression, Expression, ReadOnly, ValueType e IncludeInDebugDump.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include anche un set di variabili di sistema le cui proprietà non possono essere aggiornate, ad eccezione della proprietà RaiseChangedEvent.  
  
### <a name="set-expressions-on-variables"></a>Impostare espressioni nelle variabili  
  
 Quando si usa la finestra **Proprietà** per impostare le espressioni in una variabile definita dall'utente:  
  
-   Il valore di una variabile può essere impostato tramite la proprietà Value o Expression. Per impostazione predefinita, la proprietà valuateAsExpression è impostata su **False** e il valore della variabile è impostato dalla proprietà Value. Per impostare il valore tramite un'espressione, è necessario prima impostare EvaluateAsExpression su **True**e quindi specificare un'espressione nella proprietà Expression. La proprietà Value viene impostata automaticamente sul risultato restituito dall'espressione.  
  
-   La proprietà ValueType contiene il tipo di dati del valore della proprietà Value. Quando la proprietà Value viene impostata tramite un'espressione, la proprietà ValueType viene automaticamente aggiornata a un tipo di dati compatibile con il risultato restituito dall'espressione. Ad esempio, se la proprietà Value contiene il valore 0 e ValueType contiene **Int32** e si imposta Expression su GETDATE(), la proprietà Value conterrà la data e l'ora correnti e ValueType verrà impostata su **DateTime**.  
  
-   Tramite la finestra **Proprietà** della variabile è possibile accedere alla finestra di dialogo **Generatore di espressioni** , che consente di compilare, convalidare e valutare le espressioni. Per altre informazioni, vedere [Generatore di espressioni](../integration-services/expressions/expression-builder.md) e [Espressioni di Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 Quando si usa la finestra **Variabili** per impostare le espressioni in una variabile definita dall'utente:  
  
-   Per usare un'espressione per impostare il valore della variabile, verificare prima che il tipo di dati della variabile sia compatibile con il risultato della valutazione dell'espressione e quindi specificare un'espressione nella colonna **Espressione** della finestra **Variabili** . La proprietà EvaluateAsExpression nella finestra **Proprietà** viene automaticamente impostata su **True**.  
  
-   Quando si assegna un'espressione a una variabile, accanto a quest'ultima viene visualizzato un marcatore icona speciale. Tale marcatore icona speciale viene visualizzato anche accanto alle gestioni connessioni e alle attività in cui sono impostate espressioni.  
  
-   Tramite la finestra **Variabili** della variabile è possibile accedere alla finestra di dialogo **Generatore di espressioni** , che consente di compilare, convalidare e valutare le espressioni. Per altre informazioni, vedere [Generatore di espressioni](../integration-services/expressions/expression-builder.md) e [Espressioni di Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 In entrambe le finestre **Variabili** e **Proprietà**, se si assegna un'espressione a una variabile ed **EvaluateAsExpression** è impostato su **True**, non sarà possibile modificare il tipo di dati della variabile.  
  
### <a name="set-the-namespace-and-name-properties"></a>Impostare le proprietà Namespace e Name
  
 I valori delle proprietà **Name** e **Namespace** devono iniziare con una delle lettere dell'alfabeto definite dallo standard Unicode 2.0 oppure con un carattere di sottolineatura (_). I caratteri successivi possono includere lettere o numeri, come definito dallo standard Unicode 2.0, o il carattere di sottolineatura (\_).  
  
### <a name="set-variable-properties-in-the-variables-window"></a>Impostare le proprietà delle variabili nella finestra Variabili   
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul pacchetto in modo da aprirlo.  
  
3.  Scegliere **Variabili** dal menu **SSIS**.  
  
     Facoltativamente, è possibile visualizzare la finestra **Variabili** eseguendo il mapping del comando View.Variables a una combinazione di tasti scelta dall'utente nella pagina **Tastiera** della finestra di dialogo **Opzioni** .  
  
4.  Facoltativamente, nella finestra **Variabili** fare clic su **Opzioni griglia**, quindi selezionare le colonne che si vuole visualizzare nella finestra **Variabili** e selezionare i filtri da applicare all'elenco di variabili.  
  
5.  Selezionare la variabile nell'elenco e quindi aggiornare i valori delle colonne **Nome**, **Tipo di dati**, **Valore**, **Spazio dei nomi**, **Raise Change Event**(Genera evento di modifica), **Descrizione** ed **Espressione** .  
  
6.  Selezionare la variabile nell'elenco e quindi fare clic su **Sposta variabile** per modificarne l'ambito.  
  
7.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  
  
### <a name="set-variable-properties-in-the-properties-window"></a>Impostare le proprietà delle variabili nella finestra Proprietà  

1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul pacchetto in modo da aprirlo.  
  
3.  Scegliere **Finestra Proprietà** dal menu **Visualizza**.  
  
4.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic sulla scheda **Esplora pacchetti** ed espandere il nodo Pacchetto.  
  
5.  Per modificare le variabili con ambito pacchetto, espandere il nodo Variabili oppure espandere il nodo Gestori eventi o File eseguibili fino a individuare il nodo Variabili contenente la variabile che si desidera modificare.  
  
6.  Fare clic sulla variabile di cui si desidera modificare le proprietà.  
  
7.  Nella finestra **Proprietà** aggiornare le proprietà delle variabili in lettura/scrittura. Alcune proprietà sono di sola lettura per le variabili definite dall'utente.  
  
     Per altre informazioni sulle proprietà, vedere [Integration Services &#40;SSIS&#41; Variables](../integration-services/integration-services-ssis-variables.md).  
  
8.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  

## <a name="update-a-variable-dynamically-with-configurations"></a>Aggiornare una variabile in modo dinamico con configurazioni  
 Per aggiornare le variabili in modo dinamico, è possibile creare configurazioni per le variabili, distribuirle insieme al pacchetto e quindi aggiornare i valori delle variabili nel file di configurazione quando si distribuiscono i pacchetti. In fase di esecuzione il pacchetto utilizza i valori di variabile aggiornati. Per altre informazioni, vedere [Creazione di configurazioni dei pacchetti](../integration-services/packages/create-package-configurations.md).  

## <a name="related-tasks"></a>Attività correlate  
 [Utilizzare i valori di variabili e parametri in un pacchetto figlio](../integration-services/packages/legacy-package-deployment-ssis.md#child)  
  
 [Mapping dei parametri di query a variabili in un componente del flusso di dati](../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
