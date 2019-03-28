---
title: Caricare dati in memoria mediante rxImport RevoScaleR - SQL Server Machine Learning
description: Procedura dettagliata su come caricare i dati con il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5fc29872795623bd0d9e72414a15add92591ec7d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513018"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>Caricare dati in memoria mediante rxImport (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Il [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) funzione può essere utilizzata per spostare dati da un'origine dati in un frame di dati in memoria della sessione o in un file XDF sul disco. Se non si specifica un file come destinazione, i dati vengono inseriti in memoria come frame di dati.

In questo passaggio descrive come ottenere dati dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e quindi usare il **rxImport** funzione per inserire i dati di interesse in un file locale. In questo modo è possibile analizzare i dati nel contesto di calcolo locale più volte senza dover ripetere la query del database.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Estrarre un subset di dati da SQL Server per la memoria locale

Si è deciso che si desidera esaminare solo i clienti ad alto rischio in modo più dettagliato. La tabella di origine in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è grande, pertanto si desidera ottenere le informazioni relative solo i clienti ad alto rischio. Quindi possibile caricare i dati in un frame di dati in memoria della workstation locale.

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

3. Chiamare la funzione [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) per leggere i dati in un frame di dati nella sessione R locale.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Se l'operazione ha esito positivo, si dovrebbe vedere un messaggio di stato simile alla seguente: "Righe lette: 35, totale righe elaborate: 35, tempo di blocco totale: 0.036 seconds"

4. Ora che le osservazioni ad alto rischio si trovano in un frame di dati in memoria, è possibile usare varie funzioni R per modificare il frame di dati. Ad esempio, è possibile ordinare i clienti dal relativo punteggio di rischio e stampare l'elenco dei clienti che presentano più alto rischio.

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

Il **rxImport** funzione assegna nomi di variabile alle colonne durante il processo di importazione, ma è possibile specificare nuovi nomi di variabile con il *colInfo* parametro o tipi di dati di modifica utilizzando il *colClasses* parametro.

Specificando operazioni aggiuntive nel parametro *transforms* è anche possibile eseguire operazioni di elaborazione elementare su ogni blocco di dati che viene letto.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Creare una nuova tabella di SQL Server mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)