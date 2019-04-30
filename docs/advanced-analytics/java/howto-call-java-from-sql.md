---
title: Come chiamare Java da SQL - SQL Server Machine Learning Services
description: Informazioni su come chiamare classi Java da stored procedure SQL Server usando l'estensione del linguaggio in SQL Server 2019 di programmazione Java.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a75878ccc4f14d03f84102dd48bfd43a6e04daea
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473561"
---
# <a name="how-to-call-java-from-sql-server-2019-preview"></a>Come chiamare Java dalla versione di anteprima di SQL Server 2019

Quando si usa la [estensione del linguaggio Java](extension-java.md), il [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema stored procedure è l'interfaccia utilizzata per chiamare il runtime di Java. Autorizzazioni per il database si applicano all'esecuzione di codice Java.

Questo articolo illustra i dettagli di implementazione per le classi Java e metodi per l'esecuzione in SQL Server. Una volta acquisita familiarità con questi dettagli, esaminare i [esempio Java](java-first-sample.md) come passaggio successivo.

Esistono due metodi per la chiamata di classi Java in SQL Server:

1. Inserire i file di estensione class o con estensione jar nel [classpath Java](#classpath). È disponibile per Windows e Linux.

2. Caricamento classi compilate in un file con estensione jar e altre dipendenze nel database utilizzando la [libreria esterna](#external-library) DDL. Questa opzione è disponibile per Windows e Linux dalla versione CTP 2.4.

> [!NOTE]
> Una raccomandazione generale, usare i file con estensione jar e Class non i singoli file. Questo è pratica comune in Java e semplificano l'esperienza complessiva. Vedere anche: [Come creare un file con estensione jar dal file di classe](extension-java.md#create-jar).

<a name="classpath"></a>

## <a name="classpath"></a>Classpath

### <a name="basic-principles"></a>Principi di base

* Le classi Java personalizzate compilate devono esistere nel file Class o file con estensione jar in classpath di Java. Il [parametro CLASSPATH](#set-classpath) fornisce il percorso dei file Java compilati. 

* Nel parametro "script" per la stored procedure, è necessario specificare il metodo di Java che si sta chiamando.

* Se la classe appartiene a un pacchetto, è necessario specificare il nome "pacchetto".

* "params" viene utilizzato per passare parametri a una classe Java. Chiamata a un metodo che richiede argomenti non è supportata, che rende l'unico modo per passare i valori di argomento al metodo di parametri. 

> [!Note]
> In questa nota Riformula supportate e non supportate operazioni specifiche del linguaggio nella versione CTP 2.x.
> * La stored procedure, sono supportati i parametri di input. Non sono elencati i parametri di output.
> * Lo streaming tramite il parametro sp_execute_external_script @r_rowsPerRead non è supportato.
> * Tramite il partizionamento @input_data_1_partition_by_columns non è supportato.
> * Parallel processing usando @parallel= 1 è supportato.

### <a name="call-java-class"></a>Classe Java di chiamata

Applicabile sia Windows che Linux, il [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema stored procedure è l'interfaccia utilizzata per chiamare il runtime di Java. L'esempio seguente illustra un sp_execute_external_script usando l'estensione di Java e i parametri per la specifica di percorso, script e il codice personalizzato.

> [!NOTE]
> Si noti che non è necessario definire il metodo da chiamare. Per impostazione predefinita, un metodo chiamato **eseguire** viene chiamato. Ciò significa che è necessario seguire il SDK e implementare un metodo execute della classe Java.

```sql
DECLARE @param1 int
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>'
, @input_data_1 = N'<Input Query>'
, @param1 = @param1
```

<a name="set-classpath"></a>

### <a name="set-classpath"></a>Impostare CLASSPATH

Una volta compilate di classe Java o le classi e creato un file con estensione jar in classpath di Java, sono disponibili due opzioni per specificare il classpath per l'estensione di SQL Server Java:

**Opzione 1: Usare librerie esterne** l'opzione più semplice consiste nel rendere SQL Server consente di trovare automaticamente le classi di creazione di librerie esterne e scegliendo la libreria un file jar. [Usare librerie esterne per Java](howto-call-java-from-sql.md#external-library)

**Opzione 2: Registrare una variabile di ambiente di sistema**

Esattamente come è stato creato una variabile di ambiente di sistema per il runtime di Java, è possibile creare una variabile di ambiente di sistema e fornire i percorsi nel file con estensione jar che contiene le classi. A tale scopo, è necessario creare una variabile di ambiente system denominata "CLASSPATH".

<a name="external-library"></a>

## <a name="external-library"></a>Libreria esterna

In SQL Server 2019 CTP 2.4, è possibile usare librerie esterne per la lingua di Java in Windows e Linux. È possibile compilare le classi in un file con estensione jar e caricare il file con estensione jar e altre dipendenze nel database utilizzando la [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) DDL.

Esempio di come caricare un file con estensione jar con la libreria esterna:

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

La creazione di una libreria esterna di SQL Server hanno automaticamente accesso alle classi Java e non è necessario impostare autorizzazioni speciali al classpath.

Esempio di chiamata a un metodo in una classe da un pacchetto caricato come una libreria esterna:

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

Per altre informazioni, vedere [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="next-steps"></a>Passaggi successivi

+ [Esempio di Java in SQL Server](java-first-sample.md)
+ [Tipi di dati Java e SQL Server](java-sql-datatypes.md)
+ [Estensione del linguaggio Java in SQL Server](extension-java.md)
