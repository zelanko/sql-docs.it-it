---
title: Creazione di un'istruzione SQL (ODBC) | Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ee3dbc4c685337a930a8d7aa5ce741b2e0b876b3
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82711254"
---
# <a name="constructing-an-sql-statement-odbc"></a>Costruzione di un'istruzione SQL (ODBC)
  Le applicazioni ODBC eseguono l'accesso al database quasi sempre mediante l'esecuzione delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il formato di tali istruzioni dipende dai requisiti dell'applicazione. Le istruzioni SQL possono essere costruite nei modi seguenti:  
  
-   Hard-coded  
  
     Istruzioni statiche eseguite da un'applicazione come attività fissa.  
  
-   In fase di esecuzione  
  
     Istruzioni SQL costruite in fase di esecuzione che consentono all'utente di personalizzare l'istruzione servendosi di clausole comuni, ad esempio SELECT, WHERE e ORDER BY. Sono incluse query ad hoc immesse dagli utenti.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC del client analizza le istruzioni SQL solo per la sintassi ODBC e ISO non supportata direttamente da [!INCLUDE[ssDE](../../includes/ssde-md.md)] , in cui il driver viene trasformato [!INCLUDE[tsql](../../includes/tsql-md.md)] . Tutte le altre sintassi SQL vengono passate all'oggetto [!INCLUDE[ssDE](../../includes/ssde-md.md)] invariato, in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determinerà se è valido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questo approccio comporta due vantaggi:  
  
-   Riduzione dell'overhead  
  
     L'elaborazione dell'overhead per il driver viene ridotto al minimo, in quanto l'analisi deve essere eseguita solo per un piccolo set di clausole ODBC e ISO.  
  
-   Flessibilità  
  
     I programmatori possono personalizzare la portabilità delle applicazioni. Per migliorare la portabilità rispetto a più database, utilizzare principalmente la sintassi ODBC e ISO. Per utilizzare miglioramenti specifici di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilizzare la sintassi di [!INCLUDE[tsql](../../includes/tsql-md.md)] appropriata. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta la [!INCLUDE[tsql](../../includes/tsql-md.md)] sintassi completa, pertanto le applicazioni basate su ODBC possono sfruttare tutte le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 L'elenco di colonne di un'istruzione SELECT deve contenere solo le colonne richieste per eseguire l'attività corrente. In questo modo non solo si riduce la quantità di dati inviati attraverso la rete, ma anche l'effetto delle modifiche del database sull'applicazione. Se in un'applicazione non si fa riferimento a una colonna di una tabella, l'applicazione non viene interessata dalle modifiche apportate alla colonna.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di query &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
