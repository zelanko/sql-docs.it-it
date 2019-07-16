---
title: Costruzione di un'istruzione SQL (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
ms.assetid: 0acc71e2-8004-4dd8-8592-05c022bdd692
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa955f31d26c87b39585ddead6bc5899a9e00679
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206785"
---
# <a name="constructing-an-sql-statement-odbc"></a>Costruzione di un'istruzione SQL (ODBC)
  Le applicazioni ODBC eseguono l'accesso al database quasi sempre mediante l'esecuzione delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il formato di tali istruzioni dipende dai requisiti dell'applicazione. Le istruzioni SQL possono essere costruite nei modi seguenti:  
  
-   Hard-coded  
  
     Istruzioni statiche eseguite da un'applicazione come attività fissa.  
  
-   In fase di esecuzione  
  
     Istruzioni SQL costruite in fase di esecuzione che consentono all'utente di personalizzare l'istruzione servendosi di clausole comuni, ad esempio SELECT, WHERE e ORDER BY. Sono incluse query ad hoc immesse dagli utenti.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Client analizza le istruzioni SQL solo per la sintassi ODBC e ISO non supportati direttamente dai [!INCLUDE[ssDE](../../includes/ssde-md.md)], che il driver trasforma in [!INCLUDE[tsql](../../includes/tsql-md.md)]. Qualsiasi altra sintassi SQL viene passata al [!INCLUDE[ssDE](../../includes/ssde-md.md)] invariate, in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determina se sia valido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo approccio comporta due vantaggi:  
  
-   Riduzione dell'overhead  
  
     L'elaborazione dell'overhead per il driver viene ridotto al minimo, in quanto l'analisi deve essere eseguita solo per un piccolo set di clausole ODBC e ISO.  
  
-   Flessibilità  
  
     I programmatori possono personalizzare la portabilità delle applicazioni. Per migliorare la portabilità rispetto a più database, utilizzare principalmente la sintassi ODBC e ISO. Per utilizzare miglioramenti specifici di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilizzare la sintassi di [!INCLUDE[tsql](../../includes/tsql-md.md)] appropriata. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta l'intero [!INCLUDE[tsql](../../includes/tsql-md.md)] sintassi in modo che le applicazioni basate su ODBC possono sfruttare tutte le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 L'elenco di colonne di un'istruzione SELECT deve contenere solo le colonne richieste per eseguire l'attività corrente. In questo modo non solo si riduce la quantità di dati inviati attraverso la rete, ma anche l'effetto delle modifiche del database sull'applicazione. Se in un'applicazione non si fa riferimento a una colonna di una tabella, l'applicazione non viene interessata dalle modifiche apportate alla colonna.  
  
## <a name="see-also"></a>Vedere anche  
 [L'esecuzione di query &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
