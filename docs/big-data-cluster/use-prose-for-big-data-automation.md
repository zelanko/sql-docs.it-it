---
title: Generare codice per le attività di data wrangling
titleSuffix: Azure Data Studio
description: Questo articolo descrive come usare l'acceleratore di codice PROSE in Azure Data Studio per generare automaticamente il codice per le attività comuni di data wrangling.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e21c172bf886695a3d424d25907a0c36e4b22f20
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67957681"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>Data wrangling con l'acceleratore di codice PROSE

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'acceleratore di codice PROSE genera codice Python leggibile per le attività di data wrangling. È possibile combinare facilmente il codice generato con il codice scritto manualmente mentre si lavora in un notebook in Azure Data Studio. Questo articolo fornisce una panoramica di come usare l'acceleratore di codice.

 > [!NOTE]
 > Program Synthesis using Examples, o PROSE, è una tecnologia Microsoft che genera codice leggibile mediante intelligenza artificiale. A tale scopo, analizza la finalità di un utente e i dati, genera diversi programmi candidati e seleziona il programma migliore usando algoritmi di classificazione. Per altre informazioni sulla tecnologia PROSE, visitare la [home page di PROSE](https://microsoft.github.io/prose/).

L'acceleratore di codice è preinstallato in Azure Data Studio. È possibile importarlo come qualsiasi altro pacchetto Python nel notebook. Per convenzione e per brevità, viene importato come cx.

```python
import prose.codeaccelerator as cx
```

Nella versione corrente l'acceleratore di codice può generare in modo intelligente codice Python per le attività seguenti:

- Lettura di file di dati in un dataframe Pandas o Pyspark.
- Correzione di tipi di dati in un dataframe.
- Ricerca di espressioni regolari che rappresentano i modelli in un elenco di stringhe.

Per una panoramica generale dei metodi dell'acceleratore di codice, vedere la [documentazione](https://aka.ms/prose-codeaccelerator-overview).

## <a name="reading-data-from-a-file-to-a-dataframe"></a>Lettura di dati da un file in un dataframe

Spesso la lettura di file in un dataframe comporta l'analisi del contenuto del file e la determinazione dei parametri corretti da passare a una libreria di caricamento dei dati. A seconda della complessità del file, l'identificazione dei parametri corretti può richiedere diverse iterazioni.

L'acceleratore di codice PROSE risolve questo problema analizzando la struttura del file di dati e generando automaticamente il codice per caricare il file. Nella maggior parte dei casi, il codice generato analizza correttamente i dati. In alcuni casi potrebbe essere necessario modificare il codice per soddisfare le esigenze specifiche.

Prendere in considerazione gli esempi seguenti:

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

Il blocco di codice precedente stampa il codice Python seguente per leggere un file delimitato. Si noti che PROSE calcola automaticamente il numero di righe da ignorare, di intestazioni, di virgolette, di delimitatori e così via.

 ```python
import pandas as pd

def read_file(file):
    names = ["lat",
             "lng",
             "desc",
             "zip",
             "title"]

    df = pd.read_csv(file,
        skiprows = 11,
        header = None,
        names = names,
        quotechar = "\"",
        delimiter = "|",
        index_col = False,
        dtype = str,
        na_values = [],
        keep_default_na = False,
        skipinitialspace = True)
    return df
 ```

L'acceleratore di codice può generare codice per caricare file delimitati, JSON e a larghezza fissa in un dataframe. Per la lettura dei file a larghezza fissa `ReadFwfBuilder` accetta facoltativamente un file di schema leggibile che può essere analizzato per ottenere le posizioni delle colonne. Per altre informazioni, vedere la [documentazione](https://aka.ms/prose-codeaccelerator-docs).

## <a name="fixing-data-types-in-a-dataframe"></a>Correzione di tipi di dati in un dataframe

È comune avere un dataframe Pandas o Pyspark con tipi di dati errati. Spesso ciò si verifica spesso a causa di alcuni valori non conformi in una colonna. Di conseguenza, i valori interi vengono letti come float o stringhe e le date vengono lette come stringhe. Il lavoro richiesto per la correzione manuale dei tipi di dati è proporzionale al numero di colonne.

In questi casi, è possibile usare `DetectTypesBuilder`. Questo strumento analizza i dati e invece di correggere i tipi di dati in modalità black box, genera codice per la correzione dei tipi di dati. Questo codice funge da punto di partenza. È possibile esaminarlo, usarlo o modificarlo in base alle esigenze.

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

Per altre informazioni, vedere la [documentazione](https://aka.ms/prose-codeaccelerator-fixtypes).

## <a name="identifying-patterns-in-strings"></a>Identificazione di modelli nelle stringhe

Un altro scenario comune è quello del rilevamento di modelli in una colonna di stringhe a scopo di pulizia o raggruppamento. Si potrebbe ad esempio avere una colonna di date con date in più formati diversi. Per standardizzare i valori, potrebbe essere necessario scrivere istruzioni condizionali usando espressioni regolari.


|   |Nome                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Unknown        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22-apr-67      |
| 4 |Maya de Villiers          |19-mar-60      |

A seconda del volume e della diversità dei dati, la scrittura di espressioni regolari per modelli diversi nella colonna può richiedere molto tempo. `FindPatternsBuilder` è un potente strumento di accelerazione del codice che risolve il problema precedente generando espressioni regolari per un elenco di stringhe.

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

Ecco le espressioni regolari generate da `FindPatternsBuilder` per i dati precedenti.

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

Oltre a generare espressioni regolari, `FindPatternsBuilder` può generare anche codice per il clustering dei valori in base alle espressioni regolari generate. Può inoltre verificare che tutti i valori di una colonna siano conformi alle espressioni regolari generate. Per altre informazioni e altri scenari utili, vedere la [documentazione](https://aka.ms/prose-codeaccelerator-findpatterns).
