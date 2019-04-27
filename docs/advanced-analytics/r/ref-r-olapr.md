---
title: libreria di funzioni di olapR R - servizi di SQL Server Machine Learning
description: Introduzione alla libreria di funzioni di olapR in SQL Server 2016 R Services e SQL Server 2017 Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e5419900b8ba573ec0658a5022be68105b0b8607
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641851"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (libreria R in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**olapR** è una libreria di Microsoft delle funzioni R usati per la query MDX su un cubo OLAP di SQL Server Analysis Services. Le funzioni non supportano tutte le operazioni MDX, ma è possibile compilare query tale sezione, elaborare, drill-down, rollup e trasformare tramite pivot in base alle dimensioni. 

Questo pacchetto non è precaricato in una sessione R. Eseguire il comando seguente per caricare la libreria.

```R
library(olapR)
```

È possibile usare questa libreria nelle connessioni a un cubo OLAP di Analysis Services in tutte le versioni supportate di SQL Server. Le connessioni a un modello tabulare non sono supportate in questo momento.

## <a name="package-version"></a>Versione del pacchetto

Versione corrente è 1.0.0 in tutti i prodotti Windows-only e download che fornisce la libreria.

## <a name="full-reference-documentation"></a>Documentazione di riferimento complete

Il **olapr** libreria distribuita in vari prodotti Microsoft, ma che utilizzo è lo stesso sia ottenere la libreria in SQL Server o un altro prodotto. Perché le funzioni sono gli stessi, [documentazione per le funzioni sqlrutils singoli](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) pubblicata in un'unica posizione sotto il [riferimento R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per Microsoft Machine Learning Server. Qualsiasi prodotto specifico deve comportamenti esistono, verranno indicate nella pagina della Guida funzione discrepanze.

## <a name="availability-and-location"></a>Disponibilità e la posizione

Questo pacchetto viene fornito nei seguenti prodotti, nonché sulle diverse immagini di macchina virtuale in Azure. Percorso del pacchetto varia di conseguenza.

Prodotto | Location |
--------|----------|
SQL Server 2017 Machine Learning Services (con l'integrazione di R) | C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Programmi\Microsoft Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\library |
Macchina virtuale data Science (in Azure) | C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\library |
Macchina virtuale SQL Server (on Azure) <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> integrazione di R è facoltativo in SQL Server. La libreria olapR verrà installata quando si aggiunge la funzionalità R o il Machine Learning durante la configurazione della macchina virtuale.


## <a name="see-also"></a>Vedere anche

[Come creare query MDX con olapR](how-to-create-mdx-queries-using-olapr.md)
