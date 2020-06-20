---
title: Costrutti supportati su stored procedure compilate in modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
author: rothja
ms.author: jroth
ms.openlocfilehash: ba83dbb706b674581a35d5927639208adc061122
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025651"
---
# <a name="supported-constructs-on-natively-compiled-stored-procedures"></a>Costrutti supportati su stored procedure compilate in modo nativo
  In questo argomento vengono illustrati i costrutti supportati nelle stored procedure compilate in modo nativo.  
  
 Per altre informazioni su costrutti non supportati, vedere [Costrutti Transact-SQL non supportati da OLTP in memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
## <a name="procedure-ddl"></a>DLL di procedura  
 Sono supportati gli elementi seguenti:  
  
-   CREATE PROCEDURE  
  
-   DROP PROCEDURE  
  
-   SCHEMABINDING (obbligatorio per le stored procedure compilate in modo nativo)  
  
-   NATIVE_COMPILATION  
  
-   I parametri possono essere dichiarati come NOT NULL.  
  
-   Parametri con valori di tabella.  
  
## <a name="security"></a>Sicurezza  
 Sono supportati gli elementi seguenti:  
  
-   Per le procedure: EXECUTE AS OWNER, SELF e utente.  
  
-   Autorizzazioni GRANT e DENY per tabelle e procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [stored procedure compilate in modo nativo](natively-compiled-stored-procedures.md)  
  
  
