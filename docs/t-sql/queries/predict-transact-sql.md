---
title: PREDICT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||=azuresqldb-current||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c97363e7f13c3b42cf447ecf69929171544f3a6b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "72907253"
---
# <a name="predict-transact-sql"></a>PREDICT (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Genera un valore o punteggi stimati in base a un modello archiviato. Per altre informazioni, vedere [Assegnazione di punteggi nativi tramite la funzione T-SQL PREDICT](../../advanced-analytics/sql-native-scoring.md).

## <a name="syntax"></a>Sintassi

```
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>  
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

MODEL = @model | model_literal  
```

### <a name="arguments"></a>Argomenti

**model**

Il parametro `MODEL` viene usato per specificare il modello usato per l'assegnazione dei punteggi o la stima. Il modello viene specificato come variabile, valore letterale o espressione scalare.

L'oggetto modello può essere creato con R, Python o un altro strumento.

**data**

Il parametro DATA viene usato per specificare i dati usati per l'assegnazione dei punteggi o la stima. I dati vengono specificati nella query sotto forma di un'origine di tabella. L'origine di tabella può essere una tabella, un alias di tabella, un alias di espressione di tabella comune, una vista o una funzione con valori di tabella.

**parameters**

Il parametro PARAMETERS viene usato per specificare parametri definiti dall'utente facoltativi usati per l'assegnazione dei punteggi o la stima.

Il nome di ogni parametro è specifico per il tipo di modello. La funzione [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) in RevoScaleR, ad esempio, supporta il parametro `@computeResiduals`, che indica se è necessario calcolare i residui quando si valuta un modello di regressione logistica. Se si chiama un modello compatibile, è possibile passare il nome del parametro e il valore TRUE o FALSE alla funzione `PREDICT`.

**WITH ( <result_set_definition> )**

La clausola WITH viene usata per specificare lo schema dell'output restituito dalla funzione `PREDICT`.

Oltre alle colonne restituiti dalla funzione `PREDICT` stessa, tutte le colonne che fanno parte dell'input di dati sono disponibili per l'uso nella query.

### <a name="return-values"></a>Valori restituiti

Non è disponibile uno schema predefinito. SQL Server non convalida il contenuto del modello né i valori di colonna restituiti.

- La funzione `PREDICT` interessa le colonne come input.
- La funzione `PREDICT`, poi, genera nuove colonne. Il numero delle colonne e i tipi di dati corrispondenti dipendono dal tipo di modello usato per la stima.

Eventuali messaggi di errore correlati ai dati, al modello o al formato delle colonne vengono restituiti dalla funzione di stima sottostante associata al modello.

- Per RevoScaleR, la funzione equivalente è [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)  
- Per MicrosoftML, la funzione equivalente è [rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict)  

Non è possibile visualizzare la struttura del modello interna tramite `PREDICT`. Se si vuole comprendere il contenuto del modello stesso, è necessario caricare l'oggetto modello, deserializzarlo e usare codice R appropriato per analizzare il modello.

## <a name="remarks"></a>Osservazioni

La funzione `PREDICT` è supportata da tutte le edizioni di SQL Server 2017 o versione successiva in Windows e in Linux. La funzione `PREDICT` è supportata anche nel database SQL di Azure nel cloud. Questo supporto è attivo indipendentemente dal fatto che siano abilitate altre funzionalità di Machine Learning.

Per usare la funzione `PREDICT` non è necessario che nel server sia installato R, Python o un altro linguaggio di Machine Learning. È possibile eseguire il training del modello in un altro ambiente e salvarlo in una tabella di SQL Server per usarlo con `PREDICT` o chiamare il modello da un'altra istanza di SQL Server contenente il modello salvato.

### <a name="supported-algorithms"></a>Algoritmi supportati

Il modello da usare deve essere stato creato con uno degli algoritmi supportati del pacchetto RevoScaleR. Per l'elenco dei modelli attualmente supportati, vedere [Assegnazione dei punteggi in tempo reale](../../advanced-analytics/real-time-scoring.md).

### <a name="permissions"></a>Autorizzazioni

Per `PREDICT` non sono necessarie autorizzazioni specifiche. L'utente, tuttavia, ha bisogno dell'autorizzazione `EXECUTE` per il database e dell'autorizzazione per eseguire query su tutti i dati usati come input. Se il modello è stato archiviato in una tabella, l'utente deve anche essere in grado di leggerlo dalla tabella.

## <a name="examples"></a>Esempi

Gli esempi seguenti illustrano la sintassi per chiamare la funzione `PREDICT`.

### <a name="using-predict-in-a-from-clause"></a>Uso di PREDICT in una clausola FROM

Questo esempio fa riferimento alla funzione `PREDICT` nella clausola `FROM` di un'istruzione `SELECT`:

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

L'alias **d** specificato per l'origine di tabella nel parametro `DATA` viene usato per fare riferimento alle colonne appartenenti a dbo.mytable. L'alias **p** specificato per la funzione **PREDICT** viene usato per fare riferimento alle colonne restituite dalla funzione PREDICT.

### <a name="combining-predict-with-an-insert-statement"></a>Combinazione di PREDICT con un'istruzione INSERT

Uno dei casi d'uso più comuni per la stima consiste nella generazione di un punteggio per dati di input e quindi nell'inserimento dei valori stimati in una tabella. L'esempio seguente presuppone che l'applicazione chiamante usi una stored procedure per inserire una riga contenente il valore stimato in una tabella:

```sql
CREATE PROCEDURE InsertLoanApplication
(@p1 varchar(100), @p2 varchar(200), @p3 money, @p4 int)
AS
BEGIN
  DECLARE @model varbinary(max) = (select model
  FROM scoring_model
  WHERE model_name = 'ScoringModelV1');
  WITH d as ( SELECT * FROM (values(@p1, @p2, @p3, @p4)) as t(c1, c2, c3, c4) )

  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = d) WITH(score float) as p;
END;
```

Se la procedura accetta più righe tramite un parametro con valori di tabella, può essere scritta come segue:

```sql
CREATE PROCEDURE InsertLoanApplications (@new_applications dbo.loan_application_type)
AS
BEGIN
  DECLARE @model varbinary(max) = (SELECT model_bin FROM scoring_models WHERE model_name = 'ScoringModelV1');
  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = @new_applications as d)
  WITH (score float) as p;
END;
```

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>Creazione di un modello R e generazione di punteggi tramite parametri facoltativi del modello

Questo esempio presuppone che sia stato creato un modello di regressione logistica dotato di una matrice di covarianza tramite una chiamata a RevoScaleR simile alla seguente:

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

Se si archivia il modello in SQL Server in formato binario, è possibile usare la funzione PREDICT per generare non solo stime, ma anche informazioni aggiuntive supportate dal tipo di modello, ad esempio gli intervalli di errore o di confidenza.

Il codice seguente illustra la chiamata R equivalente a [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict):

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

La chiamata equivalente che usa la funzione `PREDICT` fornisce anche il punteggio (valore stimato), e gli intervalli di errore e di confidenza:

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```

## <a name="next-steps"></a>Passaggi successivi

- [Assegnazione di punteggi nativi tramite la funzione T-SQL PREDICT](../../advanced-analytics/sql-native-scoring.md)
