---
title: Driver basati su file | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45d9203a08b9c70809e81fb3d9cf84a521017068
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628601"
---
# <a name="file-based-drivers"></a>Driver basati su file
Driver basati su file vengono utilizzati con origini dati quali file dBASE che non si forniscono un motore di database autonomo per il driver da usare. Questi driver accedere direttamente ai dati fisici e devono implementare un motore di database per elaborare istruzioni SQL. Una procedura standard, i motori di database nei driver basati su file implementano il subset di ODBC SQL, definito dal livello di conformità SQL minima. per un elenco delle istruzioni SQL in questo livello di conformità, vedere [appendice c: Grammatica SQL](../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Nel confronto tra driver basati su DBMS e file, driver basati su file sono meno potenti e più difficili da scrivere a causa di componente del motore di database, meno complesso da configurare poiché non sono presenti network, perché alcuni utenti hanno il tempo necessario per scrivere database motori efficienti quanto quelle prodotte da società di database.  
  
 La figura seguente mostra due diverse configurazioni di driver basati su file, uno in cui i dati si trovano in locale e l'altro in cui si trova in un file server di rete.  
  
 ![Due configurazioni del file&#45;basato su driver](../../odbc/reference/media/pr06.gif "pr06")
