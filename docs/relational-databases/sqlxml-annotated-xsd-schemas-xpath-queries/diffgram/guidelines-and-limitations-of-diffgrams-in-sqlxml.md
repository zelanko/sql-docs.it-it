---
title: Linee guida e limitazioni per i Diffgram in SQLXML
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 113090c317e88d3e9a7e7db2bfcb7d4d14b4ea1f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650070"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Linee guida e limitazioni per i Diffgram in SQLXML
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Quando si utilizzano Diffgram con SQLXML 4.0, tenere presenti le considerazioni seguenti:  
  
-   I tipi di oggetti binari di grandi dimensioni (BLOB), ad esempio **text/ntext** e images, non devono essere utilizzati nel **\<diffgr:before>** blocco in quando si utilizza DiffGram, in quanto verranno inclusi per l'utilizzo nel controllo della concorrenza. Ciò può provocare problemi con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a causa delle limitazioni applicate al confronto per i tipi BLOB. La parola chiave LIKE, ad esempio, viene utilizzata nella clausola WHERE per il confronto tra colonne con tipo di dati **Text** . Tuttavia, i confronti avranno esito negativo in caso di tipi BLOB in cui le dimensioni dei dati sono maggiori di 8K.  
  
-   I caratteri speciali nei dati **ntext** possono causare problemi con SQLXML 4,0 a causa delle limitazioni del confronto per i tipi di BLOB. Ad esempio, l'utilizzo di "[Serializable]" nel **\<diffgr:before>** blocco di un DiffGram se utilizzato nel controllo della concorrenza di una colonna di tipo **ntext** avrà esito negativo con la descrizione di errore SQLOLEDB seguente:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
