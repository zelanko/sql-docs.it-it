---
title: Stored procedure compilate in modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 63a3b7b1e91323290059b5208f9c2582ced1da8c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050057"
---
# <a name="natively-compiled-stored-procedures"></a>stored procedure compilate in modo nativo
  Le stored procedure compilate in modo nativo sono stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] compilate nel codice nativo che accedono a tabelle ottimizzate per la memoria. Le stored procedure compilate in modo nativo consentono un'esecuzione efficiente delle query e della logica di business nella stored procedure. Per altri dettagli sul processo di compilazione nativa, vedere [Compilazione nativa di tabelle e stored procedure](native-compilation-of-tables-and-stored-procedures.md). Per altre informazioni sulla migrazione delle stored procedure basate su disco alle stored procedure compilate in modo nativo, vedere [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](migration-issues-for-natively-compiled-stored-procedures.md).  
  
> [!NOTE]  
>  Una differenza tra le stored procedure interpretate (basate su disco) e le stored procedure compilate in modo nativo consiste nel fatto che una stored procedure interpretata viene compilata alla prima esecuzione mentre una stored procedure compilata in modo nativo viene compilata alla creazione. Con le stored procedure compilate in modo nativo, molte condizioni di errore (overflow aritmetico, conversione dei tipi e alcune condizioni di divisione per zero) possono essere rilevate al momento della creazione e causano l'esito negativo della creazione della stored procedure compilata in modo nativo. Con le stored procedure interpretate, queste condizioni di errore in genere non causano errori alla creazione della stored procedure, ma tutte le esecuzioni avranno esito negativo.  
  
 Contenuto della sezione:  
  
-   [Creazione di stored procedure compilate in modo nativo](creating-natively-compiled-stored-procedures.md)  
  
-   [Blocchi atomici](atomic-blocks-in-native-procedures.md)  
  
-   [Costrutti supportati in stored procedure compilate in modo nativo](supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [Utilizzo di try...catch in stored procedure compilate in modo nativo](../../database-engine/using-try-catch-in-natively-compiled-stored-procedures.md)  
  
-   [Costrutti supportati su stored procedure compilate in modo nativo](supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [Stored procedure compilate in modo nativo e opzioni SET di esecuzione](natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [Procedure consigliate per chiamare stored procedure compilate in modo nativo](best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [Monitoraggio delle prestazioni di stored procedure compilate in modo nativo](monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [Chiamata di stored procedure compilate in modo nativo da applicazioni di accesso ai dati](calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle ottimizzate per la memoria](memory-optimized-tables.md)  
  
  
