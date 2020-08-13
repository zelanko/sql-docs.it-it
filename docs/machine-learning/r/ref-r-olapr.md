---
title: Pacchetto olapR R
description: olapR è un pacchetto R di Microsoft usato per eseguire query MDX su un cubo OLAP di SQL Server Analysis Services. Le funzioni non supportano tutte le operazioni MDX, ma è possibile creare query in grado di eseguire operazioni di sezionamento, estrazione, drill-down, rollup e trasformazione tramite Pivot sulle dimensioni. Il pacchetto è incluso in Machine Learning Services per SQL Server e R Services per SQL Server 2016.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 844489b4c9f3e0e92848ebb1c9cb3b725ac5fedd
ms.sourcegitcommit: d1535944bff3f2580070cc036ece30f1d43ee2ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2020
ms.locfileid: "86406164"
---
# <a name="olapr-r-package-in-sql-server-machine-learning-services"></a>olapR (pacchetto R in Machine Learning Services per SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**olapR** è un pacchetto R di Microsoft usato per eseguire query MDX su un cubo OLAP di SQL Server Analysis Services. Le funzioni non supportano tutte le operazioni MDX, ma è possibile creare query in grado di eseguire operazioni di sezionamento, estrazione, drill-down, rollup e trasformazione tramite Pivot sulle dimensioni. Il pacchetto è incluso in [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md) e [R Services per SQL Server 2016](sql-server-r-services.md).

È possibile usare questo pacchetto nelle connessioni a un cubo OLAP di Analysis Services in tutte le versioni supportate di SQL Server. Le connessioni a un modello tabulare non sono attualmente supportate.

## <a name="load-package"></a>Caricare il pacchetto

Il pacchetto **olapR** non è precaricato in una sessione R. Eseguire il comando seguente per caricare il pacchetto.

```R
library(olapR)
```

## <a name="package-version"></a>Versione pacchetto

La versione corrente è la 1.0.0 in tutti i prodotti solo Windows e in tutti i download del pacchetto.

## <a name="full-reference-documentation"></a>Documentazione di riferimento completa

Il pacchetto **olapr** è distribuito in più prodotti Microsoft, ma l'utilizzo è lo stesso indipendentemente dal fatto che sia incluso in SQL Server o in un altro prodotto. Poiché le funzioni sono le stesse, la [documentazione per le singole funzioni sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) è pubblicata in una sola posizione delle [informazioni di riferimento per R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per Microsoft Machine Learning Server. In caso di comportamenti specifici per un prodotto, le discrepanze verranno indicate nella pagina della Guida delle funzioni in questione.

## <a name="availability-and-location"></a>Disponibilità e percorsi

Questo pacchetto è disponibile nei prodotti elencati di seguito, nonché in diverse immagini di macchina virtuale in Azure. Il percorso del pacchetto varia di conseguenza.

Prodotto | Location |
--------|----------|
Machine Learning Services per SQL Server (con integrazione di R) | C:\Programmi\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Programmi\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Programmi\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Programmi\Microsoft\R Client\R_SERVER\library |
Data Science Virtual Machine (in Azure) | C:\Programmi\Microsoft\R Client\R_SERVER\library |
Macchina virtuale di SQL Server (in Azure) <sup>1</sup> | C:\Programmi\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> L'integrazione di R è facoltativa in SQL Server. Il pacchetto olapR viene installato quando si aggiunge la funzionalità Machine Learning o R durante la configurazione della macchina virtuale.


## <a name="see-also"></a>Vedere anche

[Come creare query MDX con olapR](how-to-create-mdx-queries-using-olapr.md)
