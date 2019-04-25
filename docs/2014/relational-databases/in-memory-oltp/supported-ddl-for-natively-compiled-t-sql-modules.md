---
title: Costrutti è supportato nelle Stored procedure compilate in modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc064eb8a4c6b206d3b690a4c4e7ca196c7475dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62467875"
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
 [Stored procedure compilate in modo nativo](natively-compiled-stored-procedures.md)  
  
  
