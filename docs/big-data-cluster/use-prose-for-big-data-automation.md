---
title: Generare il codice per attività di gestione dei dati
titleSuffix: Azure Data Studio
description: Questo articolo descrive come usare l'acceleratore di codice PROSE in Azure Data Studio per generare automaticamente codice per attività di gestione dei dati comuni.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: a42820199c2a481e490b510e3fd00f9dc765cb27
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030522"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>Wrangling dei dati usando i tasti di scelta rapida codice PROSE

Tasti di scelta rapida PROSE codice genera il codice Python leggibile per l'attività di gestione dei dati. Mentre si lavora in un notebook in Azure Data Studio, è possibile combinare il codice generato con il codice scritto a mano in modo trasparente. Questo articolo offre una panoramica di come è possibile utilizzare l'acceleratore di codice.

 > [!NOTE]
 > Programmare Synthesis using Examples, noto anche come PROSE, è una tecnologia Microsoft che genera il codice leggibile dall'utente tramite l'intelligenza artificiale. Esegue l'operazione per l'analisi di un utente con finalità, nonché i dati, generazione di alcuni programmi candidato e selezionando il miglior programma usando algoritmi di classificazione. Per altre informazioni sulla tecnologia PROSE, visitare il [PROSE homepage](https://microsoft.github.io/prose/).

L'acceleratore di codice sono preinstallato i Data Studio di Azure. È possibile importarlo come qualsiasi altro pacchetto di Python nel notebook. Per convenzione, viene importato come cx breve.

```python
import prose.codeaccelerator as cx
```

Nella versione corrente, l'acceleratore di codice in modo intelligente può generare codice Python per le attività seguenti:

- La lettura dei file di dati per un intervallo di Pandas o frame di dati Pyspark.
- Correzione di tipi di dati in un frame di dati.
- Ricerca di espressioni regolari che rappresentano i modelli in un elenco di stringhe.

Per ottenere una panoramica generale dei metodi di codice tasto di scelta rapida, vedere la [documentazione](https://aka.ms/prose-codeaccelerator-overview).

## <a name="reading-data-from-a-file-to-a-dataframe"></a>La lettura dei dati da un file in un frame di dati

La lettura dei file in un frame di dati comporta spesso, osservando il contenuto del file e determinare i parametri corretti da passare a una raccolta di caricamento dei dati. A seconda della complessità del file, che identifica i parametri corretti può richiedere diverse iterazioni.

Tasti di scelta rapida codice PROSE risolve questo problema, analizzare la struttura del file di dati e la generazione automatica di codice per caricare il file. Nella maggior parte dei casi, il codice generato analizza i dati in modo corretto. In alcuni casi, potrebbe essere necessario modificare il codice per soddisfare le proprie esigenze.

Si consideri l'esempio seguente:

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

Il blocco di codice precedente visualizza il seguente codice python per leggere un file delimitato da virgole. Si noti come PROSE determina automaticamente il numero di righe da ignorare, intestazioni, quotechars, delimitatori e così via.

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

Tasti di scelta rapida codice può generare codice carico delimitati, JSON e i file a larghezza fissa in un frame di dati. Per la lettura dei file a larghezza fissa, il `ReadFwfBuilder` accetta facoltativamente un file di schema leggibile dall'utente che esegue l'analisi per ottenere le posizioni di colonna. Per altre informazioni, vedere la [documentazione](https://aka.ms/prose-codeaccelerator-docs).

## <a name="fixing-data-types-in-a-dataframe"></a>Risoluzione dei tipi di dati in un frame di dati

È comune disporre di un intervallo di pandas o frame di dati pyspark con tipi di dati non corretto. Spesso, ciò si verifica a causa di alcuni sospettate valori in una colonna. Di conseguenza, numeri interi vengono letti come Float o stringhe e vengono lette le date come stringhe. L'impegno necessario per correggere manualmente i tipi di dati è proporzionale al numero di colonne.

È possibile usare il `DetectTypesBuilder` in queste situazioni. Questo strumento analizza i dati, e invece di correggere i tipi di dati in modo scatola nera, genera codice per correggere i tipi di dati. Il codice viene usato come punto di partenza. È possibile esaminare, utilizzare o modificarlo in base alle esigenze.

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

Per altre informazioni, vedere la [documentazione](https://aka.ms/prose-codeaccelerator-fixtypes).

## <a name="identifying-patterns-in-strings"></a>Identificazione dei motivi nelle stringhe

Un altro scenario comune è per rilevare modelli in una colonna stringa allo scopo di pulizia o di raggruppamento. Ad esempio, potrebbe essere una colonna di date con le date in più formati diversi. Per standardizzare i valori, si potrebbe voler scrivere istruzioni condizionali usando espressioni regolari.


|   |nome                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Unknown        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22-aprile-67      |
| 4 |Villiers de Maya          |Mar-19-60      |

A seconda del volume e la diversità dei dati, la scrittura di espressioni regolari per modelli differenti nella colonna può essere un'attività molto tempo. Il `FindPatternsBuilder` è uno strumento di accelerazione di codice avanzato che risolve il problema precedente tramite la generazione di espressioni regolari per un elenco di stringhe.

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

Di seguito sono le espressioni regolari generate dal `FindPatternsBuilder` per i dati sopra riportati.

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

Oltre alla generazione di espressioni regolari, `FindPatternsBuilder` anche possibile generare codice per il clustering di valori in base a espressioni regolari generato. Anche possibile effettuare un'asserzione che tutti i valori in una colonna siano conformi alle espressioni regolari generate. Per altre informazioni e altri scenari utili, vedere la [documentazione](https://aka.ms/prose-codeaccelerator-findpatterns).
