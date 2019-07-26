---
title: libreria di funzioni olapr R
description: Introduzione alla libreria di funzioni olapr in SQL Server 2016 R Services e SQL Server 2017 Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 674e4ed4d1967452093e81e7bb4f5518d9237cf6
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469980"
---
# <a name="olapr-r-library-in-sql-server"></a>olapr (libreria R in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapr** è una libreria Microsoft di funzioni R utilizzate per le query MDX su un cubo OLAP SQL Server Analysis Services. Le funzioni non supportano tutte le operazioni MDX, ma è possibile compilare query che sezionano, Didadi, drill-down, rollup e pivot sulle dimensioni. 

Questo pacchetto non è precaricato in una sessione di R. Eseguire il comando seguente per caricare la libreria.

```R
library(olapR)
```

È possibile utilizzare questa libreria per le connessioni a un cubo OLAP Analysis Services in tutte le versioni supportate di SQL Server. Al momento non sono supportate le connessioni a un modello tabulare.

## <a name="package-version"></a>Versione pacchetto

La versione corrente è 1.0.0 in tutti i prodotti solo Windows e i download che forniscono la libreria.

## <a name="full-reference-documentation"></a>Documentazione di riferimento completa

La  libreria olapr viene distribuita in più prodotti Microsoft, ma l'utilizzo è lo stesso se si ottiene la libreria in SQL Server o in un altro prodotto. Poiché le funzioni sono uguali, la [documentazione per le singole funzioni sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) viene pubblicata in una sola posizione sotto il [riferimento R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per Microsoft Machine Learning server. Se sono presenti comportamenti specifici del prodotto, le discrepanze verranno indicate nella pagina della guida della funzione.

## <a name="availability-and-location"></a>Disponibilità e località

Questo pacchetto viene fornito nei prodotti seguenti, oltre che in diverse immagini di macchine virtuali in Azure. Il percorso del pacchetto varia di conseguenza.

Prodotto | Location |
--------|----------|
Machine Learning Services SQL Server 2017 (con integrazione di R) | C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Programmi\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Programmi\Microsoft Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\library |
Data Science Virtual Machine (in Azure) | C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\library |
SQL Server macchina virtuale (in Azure) <sup>1</sup> | C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> l'integrazione R è facoltativa in SQL Server. La libreria olapr verrà installata quando si aggiunge la funzionalità Machine Learning o R durante la configurazione della macchina virtuale.


## <a name="see-also"></a>Vedere anche

[Come creare query MDX con olapr](how-to-create-mdx-queries-using-olapr.md)
