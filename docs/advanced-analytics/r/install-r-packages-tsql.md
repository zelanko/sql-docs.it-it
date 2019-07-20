---
title: Usare T-SQL (CREATE EXTERNAL LIBRARY) per installare i pacchetti R
description: Aggiungere nuovi pacchetti R a SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services (in-database).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/12/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f681634b9f57a5fd459e3f6452c04aba024bd297
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345309"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>Usare T-SQL (CREATE EXTERNAL LIBRARY) per installare i pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come installare nuovi pacchetti R in un'istanza di SQL Server in cui è abilitato Machine Learning. È possibile scegliere tra diversi approcci. Usare T-SQL funziona al meglio per gli amministratori di server che non hanno familiarità con R.

**Si applica a:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]  [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

L'istruzione [Create external Library](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) consente di aggiungere un pacchetto o un set di pacchetti a un'istanza o a un database specifico senza eseguire direttamente il codice R o Python. Tuttavia, questo metodo richiede la preparazione del pacchetto e autorizzazioni aggiuntive per il database.

+ Tutti i pacchetti devono essere disponibili come file compresso locale, anziché essere scaricati su richiesta da Internet.

+ Tutte le dipendenze devono essere identificate in base al nome e alla versione e incluse nel file zip. L'istruzione ha esito negativo se non sono disponibili pacchetti necessari, incluse le dipendenze dei pacchetti downstream. 

+ È necessario essere **db_owner** o disporre dell'autorizzazione Create external Library in un ruolo del database. Per informazioni dettagliate, vedere [Create external Library](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="download-packages-in-archive-format"></a>Scarica i pacchetti in formato di archivio

Se si sta installando un singolo pacchetto, scaricare il pacchetto in formato compresso.

È più comune installare più pacchetti a causa delle dipendenze del pacchetto. Quando un pacchetto richiede altri pacchetti, è necessario verificare che tutti siano accessibili tra loro durante l'installazione. Si consiglia di [creare un repository locale](create-a-local-package-repository-using-minicran.md) usando [miniCRAN](https://andrie.github.io/miniCRAN/) per assemblare una raccolta completa di pacchetti, nonché [igraph](https://igraph.org/r/) per l'analisi delle dipendenze dei pacchetti. L'installazione di una versione errata di un pacchetto o l'omissione di una dipendenza del pacchetto può causare la mancata riuscita di un'istruzione CREATE EXTERNAL LIBRARY. 

## <a name="copy-the-file-to-a-local-folder"></a>Copiare il file in una cartella locale

Copiare il file compresso contenente tutti i pacchetti in una cartella locale nel server. Se non si ha accesso al file system sul server, è anche possibile passare un pacchetto completo come variabile, usando un formato binario. Per ulteriori informazioni, vedere [Create external Library](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="run-the-statement-to-upload-packages"></a>Eseguire l'istruzione per caricare i pacchetti

Aprire una finestra di **query** usando un account con privilegi amministrativi.

Eseguire l'istruzione `CREATE EXTERNAL LIBRARY` T-SQL per caricare la raccolta di pacchetti compresso nel database.

Ad esempio, l'istruzione seguente chiama come origine del pacchetto un repository miniCRAN contenente il pacchetto **randomForest** , insieme alle relative dipendenze. 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

Non è possibile usare un nome arbitrario; il nome della libreria esterna deve avere lo stesso nome che si prevede di usare per il caricamento o la chiamata del pacchetto.

## <a name="verify-package-installation"></a>Verificare l'installazione del pacchetto

Se la libreria viene creata correttamente, è possibile eseguire il pacchetto in SQL Server, chiamandolo all'interno di un stored procedure.
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>Vedere anche

+ [Ottenere informazioni sui pacchetti](../package-management/installed-package-information.md)
+ [Esercitazioni di R](../tutorials/sql-server-r-tutorials.md)
