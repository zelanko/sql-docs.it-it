---
description: Dimensioni della colonna VARCHAR (driver ODBC per Oracle)
title: Dimensioni colonne VARCHAR (driver ODBC per Oracle) | Microsoft Docs
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
ms.openlocfilehash: c490487f0edb15fe7d7165b79c4c5f1730a0dd22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449063"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Dimensioni della colonna VARCHAR (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 In Oracle8 la dimensione massima di una colonna VARCHAR è aumentata da 2000 a 4000 byte. Il software client Oracle 7.3. x non è in grado di associare un valore di parametro superiore a 2000 byte. Se pertanto si crea una tabella con una colonna VARCHAR superiore a 2000 byte, non sarà possibile eseguire inserimenti, aggiornamenti, eliminazioni e query con parametri con dati che superano il limite di 2000 byte del software client. Poiché il driver ODBC per Oracle e il provider OLE DB per Oracle utilizzano inserimenti, aggiornamenti, eliminazioni e query con parametri, verranno segnalati gli errori di ORA-01026 in questo caso. I dati che rientrano nei limiti applicati dal software client Oracle funzioneranno. Per evitare questo limite di 2000 byte, è necessario aggiornare il software client a Oracle8 (8.0.4.1.1 c o versione successiva).
