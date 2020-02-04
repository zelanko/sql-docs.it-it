---
title: Libreria di funzioni R olapR
description: Introduzione alla libreria di funzioni olapR in R Services per SQL Server 2016 e in Machine Learning Services per SQL Server con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 507bd04140880a3c15f1e72eed49c29ade56769c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68715003"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (libreria R in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapR** è una libreria Microsoft di funzioni R usate per eseguire query MDX su un cubo OLAP di SQL Server Analysis Services. Le funzioni non supportano tutte le operazioni MDX, ma è possibile creare query in grado di eseguire operazioni di sezionamento, estrazione, drill-down, rollup e trasformazione tramite Pivot sulle dimensioni. 

Questo pacchetto non viene precaricato in una sessione di R. Eseguire il comando seguente per caricare la libreria.

```R
library(olapR)
```

È possibile usare questa libreria nelle connessioni a un cubo OLAP di Analysis Services in tutte le versioni supportate di SQL Server. Le connessioni a un modello tabulare non sono attualmente supportate.

## <a name="package-version"></a>Versione pacchetto

La versione corrente corrisponde alla versione 1.0.0 in tutti i prodotti solo Windows e in tutti i download della libreria.

## <a name="full-reference-documentation"></a>Documentazione di riferimento completa

La libreria **olapr** è distribuita in più prodotti Microsoft, ma l'utilizzo è lo stesso indipendentemente dal fatto che sia inclusa in SQL Server o in un altro prodotto. Poiché le funzioni sono le stesse, la [documentazione per le singole funzioni sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) è pubblicata in una sola posizione delle [informazioni di riferimento per R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per Microsoft Machine Learning Server. In caso di comportamenti specifici per un prodotto, le discrepanze verranno indicate nella pagina della Guida delle funzioni in questione.

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

<sup>1</sup> L'integrazione di R è facoltativa in SQL Server. La libreria olapr viene installata quando si aggiunge la funzionalità Machine Learning o R durante la configurazione della macchina virtuale.


## <a name="see-also"></a>Vedere anche

[Come creare query MDX con olapR](how-to-create-mdx-queries-using-olapr.md)
