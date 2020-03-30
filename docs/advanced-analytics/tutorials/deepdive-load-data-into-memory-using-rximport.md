---
title: Caricare i dati mediante rxImport
description: 'Esercitazione di RevoScaleR 10: Come caricare i dati usando il linguaggio R in SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b9b3924f2c9b315e519d5f65e68d2006a2a6edf4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "74947077"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>Caricare dati in memoria usando rxImport (esercitazione su SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa è l'esercitazione 10 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Questa esercitazione illustrerà come ottenere i dati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usare la funzione **rxImport** per inserire i dati di interesse in un file locale. In questo modo è possibile analizzare i dati nel contesto di calcolo locale più volte senza dover ripetere la query del database.

La funzione [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) può essere usata per spostare i dati da un'origine dati di un frame di dati nella memoria di una sessione o in un file XDF sul disco. Se non si specifica un file come destinazione, i dati vengono inseriti in memoria come frame di dati.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Estrarre un subset di dati da SQL Server alla memoria locale

Si è deciso di esaminare in maggior dettaglio solo i clienti ad alto rischio. La tabella di origine di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è particolarmente grande e si vuole quindi ottenere informazioni solo sui clienti ad alto rischio. I dati vengono quindi caricati in un frame di dati nella memoria della workstation locale.

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

3. Chiamare la funzione [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) per caricare i dati in un frame di dati nella sessione R locale.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Se l'operazione ha esito positivo, verrà visualizzato un messaggio di stato simile al seguente: "Rows Read: 35, Total Rows Processed: 35, Total Chunk Time: 0.036 seconds"

4. Ora che il frame di dati in memoria contiene le osservazioni con i punteggi di rischio più alti, è possibile usare varie funzioni R per gestire il frame di dati. È possibile, ad esempio, classificare i clienti in base al punteggio di rischio e stampare l'elenco dei clienti con il rischio più elevato.

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

La funzione **rxImport** assegna nomi di variabile alle colonne durante il processo di importazione, ma è possibile specificare nuovi nomi di variabile con il parametro *colInfo* o modificare i tipi di dati con il parametro *colClasses*.

Specificando operazioni aggiuntive nel parametro *transforms* è anche possibile eseguire operazioni di elaborazione elementare su ogni blocco di dati che viene letto.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare una nuova tabella di SQL Server mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)