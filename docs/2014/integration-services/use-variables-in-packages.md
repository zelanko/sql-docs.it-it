---
title: Usare le variabili nei pacchetti | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined variables [Integration Services]
- variables [Integration Services], use scenarios
- system variables [Integration Services]
ms.assetid: 7742e92d-46c5-4cc4-b9a3-45b688ddb787
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 910d1699c8cd88f9f29d22b7f08a80337a25473d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62926327"
---
# <a name="use-variables-in-packages"></a>Utilizzo di variabili nei pacchetti
  Le variabili rappresentano un elemento aggiuntivo utile e flessibile dei pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Consentono infatti la comunicazione tra i vari oggetti di un pacchetto e tra pacchetti padre e figlio. Le variabili possono essere utilizzate anche in espressioni e script.  
  
## <a name="user-defined-variables-and-system-variables"></a>Variabili definite dall'utente e variabili di sistema  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] supporta variabili di sistema e variabili definite dall'utente. Quando si crea un nuovo pacchetto, si aggiunge un contenitore o un'attività a un pacchetto oppure si crea un gestore dell'evento, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include un set di variabili di sistema per il contenitore. Le variabili di sistema contengono informazioni utili su pacchetto, contenitore, attività o gestore dell'evento. Ad esempio, in fase di esecuzione la variabile di sistema **MachineName** include il nome del computer su cui è in esecuzione il pacchetto mentre la variabile **StartTime** include l'ora di inizio dell'esecuzione del pacchetto. Le variabili di sistema sono di sola lettura. Per altre informazioni, vedere [Variabili di sistema](system-variables.md).  
  
 È possibile creare variabili definite dall'utente e utilizzarle quindi nei pacchetti. In [!INCLUDE[ssIS](../includes/ssis-md.md)]queste variabili possono essere incluse negli script, nelle espressioni usate da vincoli di precedenza, nel contenitore Ciclo For, nelle trasformazioni Colonna derivata e Suddivisione condizionale, nonché nelle espressioni di proprietà per l'aggiornamento dei valori delle proprietà.  
  
 È possibile, ad esempio, includere una variabile definita dall'utente nella condizione di valutazione per il contenitore Ciclo For. È inoltre possibile eseguire il mapping tra il valore della raccolta di enumeratori di un contenitore Ciclo Foreach e una variabile e, se un'attività Esegui SQL utilizza un'istruzione SQL con parametri, è possibile eseguire il mapping tra parametri dell'istruzione e variabili. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md).  
  
## <a name="variables-usage-scenarios"></a>Scenari di utilizzo delle variabili  
 Nei pacchetti [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] le variabili vengono utilizzate in diversi modi. Durante lo sviluppo di un pacchetto vengono in genere aggiunte variabili definite dall'utente allo scopo di implementare la flessibilità e la gestibilità richieste dalla soluzione. A seconda dello scenario, vengono comunemente utilizzate anche variabili di sistema.  
  
 **Espressioni di proprietà** Usano le variabili per specificare i valori nelle espressioni di proprietà che impostano gli oggetti e le proprietà dei pacchetti. L'espressione `SELECT * FROM @varTableName` , ad esempio, include la variabile `varTableName` che aggiorna l'istruzione SQL eseguita da un'attività Esegui SQL. L'espressione `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`" aggiorna il pacchetto eseguito dall'attività Esegui pacchetto, eseguendo il pacchetto specificato nella variabile `varPackageFirst` il primo giorno del mese e il pacchetto specificato nella variabile `varPackageOther` in altri giorni. Per altre informazioni, vedere [Utilizzo delle espressioni di proprietà nei pacchetti](expressions/use-property-expressions-in-packages.md).  
  
 **Espressioni del flusso di dati** Usano le variabili per specificare valori nelle espressioni usate dalle trasformazioni Colonna derivata e Suddivisione condizionale per popolare le colonne o per indirizzare le righe di dati nell'output di altre trasformazioni. L'espressione `@varSalutation + LastName`, ad esempio, concatena il valore della variabile `VarSalutation` e della colonna `LastName` . L'espressione `Income < @HighIncome` indirizza in un output le righe di dati in cui il valore della colonna `Income` è minore del valore della variabile `HighIncome`. Per altre informazioni, vedere [Trasformazione Colonna derivata](data-flow/transformations/derived-column-transformation.md), [Trasformazione Suddivisione condizionale](data-flow/transformations/conditional-split-transformation.md), e [Espressioni di Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 **Espressioni di vincoli di precedenza** Forniscono i valori da usare nei vincoli di precedenza per determinare se l'eseguibile soggetto al vincolo verrà eseguito o meno. Le espressioni possono essere utilizzate insieme al risultato di un'esecuzione (esito positivo, esito negativo, completamento) o in sostituzione di tale risultato. Se ad esempio l'espressione `@varMax > @varMin` restituisce `true`, l'eseguibile verrà eseguito. Per altre informazioni, vedere [Aggiunta di espressioni ai vincoli di precedenza](control-flow/precedence-constraints.md).  
  
 **Parametri e codici restituiti** Forniscono i valori ai parametri di input o archiviano i valori dei parametri di output e i codici restituiti. A tale scopo viene eseguito il mapping delle variabili ai parametri e ai valori restituiti. Se ad esempio si imposta la variabile `varProductId` su 23 e si esegue l'istruzione SQL `SELECT * from Production.Product WHERE ProductID = ?`, la query recupera il prodotto il cui `ProductID` ha valore 23. Per altre informazioni, vedere [Attività Esegui SQL](control-flow/execute-sql-task.md) e [Parametri e codici restituiti nell'attività Esegui SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
 **Espressioni del Ciclo For** Forniscono i valori da usare nell'inizializzazione, la valutazione e l'assegnazione di espressioni del Ciclo For. Se ad esempio la variabile `varCount` è uguale a 2 e `varMaxCount` è uguale a 10, l'espressione di inizializzazione è `@varCount`, quella di valutazione è  `@varCount < @varMaxCount`e quella di assegnazione è `@varCount =@varCount +1`, pertanto il ciclo si ripete 8 volte. Per altre informazioni, vedere [Contenitore Ciclo For](control-flow/for-loop-container.md).  
  
 **Configurazioni Variabile pacchetto padre** Passano i valori dai pacchetti padre ai pacchetti figlio. Queste configurazioni consentono ai pacchetti figlio di accedere alle variabili del pacchetto padre. Se ad esempio il pacchetto figlio deve utilizzare la stessa data del pacchetto padre, sarà possibile definire un tipo di configurazione Variabile pacchetto padre che specifichi un set di variabili tramite la funzione GETDATE nel pacchetto padre. Per altre informazioni, vedere [Attività Esegui pacchetto](control-flow/execute-package-task.md) e [Configurazioni di pacchetto](../../2014/integration-services/package-configurations.md).  
  
 **Attività Script e componente script** Forniscono un elenco di variabili di sola lettura e di lettura/scrittura all'attività Script o al componente script, aggiornano le variabili di lettura/scrittura all'interno dello script, quindi usano i valori aggiornati all'interno o all'esterno dello script. Ad esempio, nel codice `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`la variabile di script `numberOfCars` viene aggiornata dal valore della variabile `NumberOfCars`. Per altre informazioni, vedere [Utilizzo di variabili nell'attività Script](control-flow/script-task.md).  
  
## <a name="configurations-and-variables"></a>Configurazioni e variabili  
 Per aggiornare le variabili in modo dinamico, è possibile creare configurazioni per le variabili, distribuirle insieme al pacchetto e quindi aggiornare i valori delle variabili nel file di configurazione quando si distribuiscono i pacchetti. In fase di esecuzione il pacchetto utilizza i valori di variabile aggiornati. Per altre informazioni, vedere [Creazione di configurazioni dei pacchetti](../../2014/integration-services/create-package-configurations.md).  
  
### <a name="to-add-modify-and-delete-user-defined-variables"></a>Per aggiungere, modificare ed eliminare variabili definite dall'utente  
  
-   [Aggiungere, eliminare o modificare l'ambito di una variabile definita dall'utente in un pacchetto](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
-   [Impostazione delle proprietà di una variabile definita dall'utente](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
  
