---
title: Dimensioni della colonna VARCHAR (Driver ODBC per Oracle) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db2871324f92ef6d84a8bf8313db105489100a96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232165"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Dimensioni della colonna VARCHAR (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 In Oracle8, le dimensioni massime di una colonna VARCHAR sono aumentato da 2000 a 4000 byte. Il software client di 7.3.x Oracle non dispone di alcun modo per associare un valore di parametro superiore a 2000 byte. Pertanto, se si crea una tabella con una colonna VARCHAR di dimensioni superiori a 2000 byte, non sarà possibile eseguire con parametri inserimenti, aggiornamenti, eliminazioni e query su di essa con i dati che superano il limite di 2000-byte del software client. Perché sia il Driver ODBC per Oracle e il Provider OLE DB per Oracle di usare le query, gli aggiornamenti, eliminazioni e inserimenti con parametri, essi verranno segnalati gli errori o un 01026 in questo caso. I dati entro i limiti applicati dal software client Oracle funzionerà. Per evitare il limite di 2000 byte, è necessario aggiornare il software client a Oracle8 (8.0.4.1.1c o versione successiva).
