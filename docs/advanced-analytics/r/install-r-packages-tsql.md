---
title: Usare T-SQL (CREATE EXTERNAL LIBRARY) per installare pacchetti R - servizi di SQL Server Machine Learning
description: Aggiungere nuovi pacchetti R per SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services (In-Database).
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b59f15ace1dc96af537486336e76a209f1c85da7
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510275"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>Usare T-SQL (CREATE EXTERNAL LIBRARY) per installare pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come installare nuovi pacchetti R in un'istanza di SQL Server in cui è abilitata l'apprendimento automatico. Sono disponibili più approcci tra cui scegliere. Usando T-SQL è adatta per gli amministratori del server che non hanno familiarità con R.

**Si applica a:**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Il [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) istruzione consente di aggiungere un pacchetto o un set di pacchetti a un'istanza o un database specifico senza esecuzione di R o Python code direttamente. Tuttavia, questo metodo richiede la preparazione del pacchetto e le autorizzazioni di database aggiuntivo.

+ Tutti i pacchetti devono essere disponibile come un file compresso locale, anziché scaricato su richiesta da internet.

+ Tutte le dipendenze devono essere identificate dal nome e la versione e inclusi nel file con estensione zip. L'istruzione ha esito negativo se i pacchetti richiesti non sono disponibili, tra cui le dipendenze dei pacchetti a valle. 

+ È necessario essere **db_owner** o disporre dell'autorizzazione CREATE EXTERNAL LIBRARY in un ruolo del database. Per informazioni dettagliate, vedere [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="download-packages-in-archive-format"></a>Scaricare i pacchetti in formato di archiviazione

Se si installa un pacchetto singolo, scaricare il pacchetto in formato compresso.

È più comune per installare i pacchetti più a causa di dipendenze di pacchetto. Quando un pacchetto richiede altri pacchetti, è necessario verificare che tutti gli elementi sono accessibili tra loro durante l'installazione. È consigliabile [creazione di un repository locale](create-a-local-package-repository-using-minicran.md) utilizzando [miniCRAN](https://andrie.github.io/miniCRAN/) assemblare una completa raccolta di pacchetti, nonché [igraph](https://igraph.org/r/) per l'analisi delle dipendenze dei pacchetti. Installazione della versione errata di un pacchetto o l'omissione di una dipendenza del pacchetto può causare un esito negativo dell'istruzione CREATE EXTERNAL LIBRARY. 

## <a name="copy-the-file-to-a-local-folder"></a>Copiare il file in una cartella locale

Copiare il file compresso che contiene tutti i pacchetti in una cartella locale nel server. Se non si ha accesso al file system nel server, è anche possibile passare un pacchetto completo come variabile, usando un formato binario. Per altre informazioni, vedere [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="run-the-statement-to-upload-packages"></a>Eseguire l'istruzione per caricare i pacchetti

Aprire una **Query** finestra utilizzando un account con privilegi amministrativi.

Eseguire l'istruzione T-SQL `CREATE EXTERNAL LIBRARY` per caricare la raccolta di pacchetti compresso del database.

Ad esempio, l'istruzione seguente nomi, come origine del pacchetto, di un repository miniCRAN contenenti i **randomForest** pacchetto, insieme alle relative dipendenze. 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

Non è possibile usare un nome arbitrario. il nome della libreria esterna deve avere lo stesso nome che si prevede di usare durante il caricamento o la chiamata del pacchetto.

## <a name="verify-package-installation"></a>Verificare l'installazione del pacchetto

Se la libreria è stata creata, è possibile eseguire il pacchetto in SQL Server, effettuando una chiamata all'interno di una stored procedure.
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>Vedere anche

+ [Ottenere informazioni sui pacchetti](determine-which-packages-are-installed-on-sql-server.md)
+ [Esercitazioni di R](../tutorials/sql-server-r-tutorials.md)
+ [Guide pratiche](sql-server-machine-learning-tasks.md)