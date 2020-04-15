---
title: Dimensione colonna VARCHAR (driver ODBC per Oracle) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11e1de3171521c57c80beb207d33e67d26d3e33
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304826"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Dimensioni della colonna VARCHAR (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 In Oracle8, la dimensione massima di una colonna VARCHAR è aumentata da 2000 a 4000 byte. Il software client Oracle 7.3.x non ha modo di associare un valore di parametro maggiore di 2000 byte. Pertanto, se si crea una tabella con una colonna VARCHAR di dimensioni superiori a 2000 byte, non sarà possibile eseguire inserimenti con parametri, aggiornamenti, eliminazioni ed esegue query su di essa con dati che superano il limite di 2000 byte del software client. Poiché sia il driver ODBC per Oracle che il provider OLE DB per Oracle utilizzano inserimenti, aggiornamenti, eliminazioni e query con parametri, in questo caso verranno segnalati errori ORA-01026. I dati che rientrano nei limiti immati dal software client Oracle funzioneranno. Per evitare questo limite di 2000 byte, è necessario aggiornare il software client a Oracle8 (8.0.4.1.1c o superiore).
