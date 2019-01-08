---
title: Come chiamare Java da SQL - SQL Server Machine Learning Services
description: Informazioni su come chiamare classi Java da stored procedure SQL Server usando l'estensione del linguaggio in SQL Server 2019 di programmazione Java.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/07/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 438c1096a933932e08c5cbf21722ba75874bb1dc
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644760"
---
# <a name="how-to-call-java-from-sql-server-2019-preview"></a>Come chiamare Java dalla versione di anteprima di SQL Server 2019

Quando si usa la [estensione del linguaggio Java](extension-java.md), il [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema stored procedure è l'interfaccia utilizzata per chiamare il runtime di Java. Autorizzazioni per il database si applicano all'esecuzione di codice Java.

Questo articolo illustra i dettagli di implementazione per le classi Java e metodi per l'esecuzione in SQL Server. Una volta acquisita familiarità con questi dettagli, esaminare i [esempio Java](java-first-sample.md) come passaggio successivo.

## <a name="basic-principles"></a>Principi di base

* Le classi Java personalizzate compilate devono esistere nel file Class o file con estensione jar in classpath di Java. Il [parametro CLASSPATH](#set-classpath) fornisce il percorso dei file Java compilati. 

* Nel parametro "script" per la stored procedure, è necessario specificare il metodo di Java che si sta chiamando.

* Se la classe appartiene a un pacchetto, è necessario specificare il nome "pacchetto".

* "params" viene utilizzato per passare parametri a una classe Java. Chiamata a un metodo che richiede argomenti non è supportata, che rende l'unico modo per passare i valori di argomento al metodo di parametri. 

> [!Note]
> In questa nota Riformula supportate e non supportate operazioni specifiche del linguaggio nella versione CTP 2.x.
> * La stored procedure, sono supportati i parametri di input. Non sono elencati i parametri di output.
> * Lo streaming tramite il parametro sp_execute_external_script **@r_rowsPerRead** non è supportato.
> * Tramite il partizionamento **@input_data_1_partition_by_columns** non è supportato.
> * Parallel processing usando  **@parallel= 1** è supportata.

## <a name="call-spexecuteexternalscript"></a>Chiamata di sp_execute_external_script

Applicabile sia Windows che Linux, il [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema stored procedure è l'interfaccia utilizzata per chiamare il runtime di Java. L'esempio seguente illustra un sp_execute_external_script usando l'estensione di Java e i parametri per la specifica di percorso, script e il codice personalizzato.

```sql
DECLARE @myClassPath nvarchar(30)
DECLARE @param1 int

SET @myClassPath = N'/<my path>/program.jar'
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>.<methodName>'
, @input_data_1 = N'<Input Query>
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @param1
```

<a name="set-classpath"></a>

## <a name="set-classpath"></a>Impostare CLASSPATH

Dopo aver compilato la classe Java o le classi e inseriti i file con estensione class o il file con estensione jar in classpath di Java, sono disponibili due opzioni per specificare il classpath per l'estensione di SQL Server Java:

**Opzione 1: Passare come parametro**

Uno degli approcci che consentono di specificare un percorso di codice compilato è tramite l'impostazione CLASSPATH come parametro di input per la procedura di sp_execute_external_script. Il [esempio Java](java-first-sample.md#call-method) questa tecnica è dimostrata. Se si sceglie questo approccio e con più percorsi, assicurarsi di usare il separatore di percorso valido per il sistema operativo sottostante:

* In Linux, separare i percorsi in CLASSPATH con due punti ":".
* In Windows, separare i percorsi nel CLASSPATH con un punto e virgola ";"

**Opzione 2: Registrare una variabile di sistema**

Esattamente come una variabile di sistema per i file eseguibili JDK è stato creato, è possibile creare una variabile di sistema per i percorsi del codice. A tale scopo, creati una variabile di ambiente system denominata "CLASSPATH"

## <a name="class-requirements"></a>Requisiti della classe

Perché SQL Server comunicare con il runtime di Java, è necessario implementare le variabili statiche specifiche nella classe. SQL Server possono quindi eseguire un metodo nei dati di classe e lo scambio di Java usando l'estensione del linguaggio Java.

> [!Note]
> Prevedere i dettagli di implementazione per modificare nelle prossime versioni CTP come Microsoft si impegna per migliorare l'esperienza per gli sviluppatori.

## <a name="method-requirements"></a>Requisiti del metodo
Per passare argomenti, usare il **@param** parametro in sp_execute_external_script. Il metodo di stesso non può avere argomenti. Il tipo restituito deve essere void.  

```java
public static void test()  {}
```

## <a name="data-inputs"></a>Input di dati 

Questa sezione viene illustrato come eseguire il push dei dati a Java da una query di SQL Server tramite **InputDataSet** in sp_execute_external_script.

Per ogni colonna di input che nella query SQL effettua il push di Java, è necessario dichiarare una matrice.

### <a name="inputdatacol"></a>inputDataCol

Nella versione corrente dell'estensione Java, il **inputDataColN** variabile è obbligatoria, in cui *N* è il numero di colonna. 

```java
public static <type>[] inputDataColN = new <type>[1]
```

Questi array devono essere inizializzati (la dimensione della matrice deve essere maggiore di 0 e non dispone in modo da riflettere la lunghezza effettiva della colonna).

Esempio: `public static int[] inputDataCol1 = new int[1];`

Queste variabili di matrice verranno popolate con dati di input da una query di SQL server prima dell'esecuzione del programma Java che si sta chiamando.

### <a name="inputnullmap"></a>inputNullMap

Mappa null viene utilizzata dall'estensione per sapere quali valori sono null. Questa variabile verrà popolata con informazioni sui valori null da SQL Server prima dell'esecuzione della funzione utente.

L'utente deve solo inizializzare la variabile e la dimensione della matrice deve essere maggiore di 0.

```java
public static boolean[][] inputNullMap = new boolean[1][1];
```

## <a name="data-outputs"></a>Output di dati 

Questa sezione vengono descritte **OutputDataSet**, i set di dati di output restituito da Java, che è possibile inviare a e salvare in modo permanente in SQL Server.

> [!Note]
> I parametri in di output [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) non sono supportati in questa versione.

### <a name="outputdatacoln"></a>outputDataColN

Simile a **inputDataSet**, per ogni colonna di output dell'applicazione Java invia al Server SQL, è necessario dichiarare una variabile di matrice. Tutti i **outputDataCol** matrici devono avere la stessa lunghezza. È necessario assicurarsi che questo venga inizializzato nel momento in cui che termina l'esecuzione di classe.

```java
public static <type>[] outputDataColN = new <type>[]
```

### <a name="numberofoutputcols"></a>numberofOutputCols

Impostare questa variabile per il numero di colonne di dati di output che si prevede che al termine dell'esecuzione della funzione utente.

```java
public static short numberofOutputCols = <expected number of output columns>;
```

### <a name="outputnullmap"></a>outputNullMap

Mappa null viene utilizzata dall'estensione per indicare quali valori sono null. È necessario poiché i tipi primitivi non supportano null. Attualmente, è necessario anche che la mappa null per i tipi di stringa, anche se le stringhe possono essere null. I valori null sono indicati da "true".

Questo NullMap deve essere popolato con il numero previsto di colonne e righe che si restituisce a SQL Server.

```java
public static boolean[][] outputNullMap
```
<a name="create-external-library"></a>


## <a name="next-steps"></a>Passaggi successivi

+ [Esempio di Java in SQL Server](java-first-sample.md)
+ [Tipi di dati Java e SQL Server](java-sql-datatypes.md)
+ [Estensione del linguaggio Java in SQL Server](extension-java.md)
