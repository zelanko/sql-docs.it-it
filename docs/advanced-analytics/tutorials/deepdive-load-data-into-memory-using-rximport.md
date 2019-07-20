---
title: Caricare i dati in memoria usando RevoScaleR rxImport
description: Esercitazione dettagliata su come caricare i dati usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: fb98887d9cfd3f1997ce82620eeff5df98ba6b1e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344668"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>Caricare i dati in memoria usando rxImport (esercitazione SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questa lezione fa parte dell' [esercitazione su RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare le [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

La funzione [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) può essere usata per spostare i dati da un'origine dati in un frame di dati nella memoria della sessione o in un file XDF su disco. Se non si specifica un file come destinazione, i dati vengono inseriti in memoria come frame di dati.

In questo passaggio si apprenderà come ottenere i dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]da e quindi usare la funzione **rxImport** per inserire i dati di interesse in un file locale. In questo modo è possibile analizzare i dati nel contesto di calcolo locale più volte senza dover ripetere la query del database.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Estrarre un subset di dati dal SQL Server alla memoria locale

Si è deciso di voler esaminare più in dettaglio solo le persone ad alto rischio. La tabella di origine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in è grande, pertanto si desidera ottenere le informazioni relative solo ai clienti ad alto rischio. I dati vengono quindi caricati in un frame di dati nella memoria della workstation locale.

1. Ripristinare il contesto di calcolo impostandolo sulla workstation locale.

    ```R
    rxSetComputeContext("local")
    ```

2. Creare un nuovo oggetto origine dati SQL Server specificando un'istruzione SQL valida nel parametro *sqlQuery* . Con questo esempio si ottiene un subset delle osservazioni con i punteggi di rischio più alti. In tal modo vengono inseriti nella memoria locale solo i dati effettivamente necessari.

    ```R
    sqlServerProbDS \<- RxSqlServerData(
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)
    ```

3. Chiamare la funzione [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) per leggere i dati in un frame di dati nella sessione di R locale.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Se l'operazione ha esito positivo, verrà visualizzato un messaggio di stato simile al seguente: "Righe lette: 35, totale righe elaborate: 35, tempo totale blocco: 0,036 secondi "

4. Ora che le osservazioni ad alto rischio si trovano in un frame di dati in memoria, è possibile usare varie funzioni R per modificare il frame di dati. Ad esempio, è possibile ordinare i clienti in base al Punteggio di rischio e stampare un elenco dei clienti che presentano il rischio più elevato.

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**Risultati**

```R
ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1
9.786345    SD   Male  Principal   23456       25            5 75   0.99994382
9.433040    FL Female  Principal   20629       24           28 75   0.99992003
8.556785    NY Female  Principal   19064       82           53 43   0.99980784
8.188668    AZ Female  Principal   19948       29            0 75   0.99972235
7.551699    NY Female  Principal   11051       95            0 75   0.99947516
7.335080    NV   Male  Principal   21566        4            6  75   0.9993482
```

## <a name="more-about-rximport"></a>Altre informazioni su rxImport

La funzione **rxImport** può essere usata non solo per spostare i dati, ma anche per trasformarli durante il processo di lettura. È ad esempio possibile specificare il numero di caratteri per le colonne a larghezza fissa, includere una descrizione delle variabili, impostare i livelli per le colonne di fattori, nonché creare nuovi livelli da usare dopo l'importazione.

La funzione **rxImport** assegna i nomi delle variabili alle colonne durante il processo di importazione, ma è possibile indicare i nuovi nomi delle variabili tramite il parametro *colInfo* o modificare i tipi di dati utilizzando il parametro *colClasses* .

Specificando operazioni aggiuntive nel parametro *transforms* è anche possibile eseguire operazioni di elaborazione elementare su ogni blocco di dati che viene letto.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare una nuova tabella di SQL Server mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)