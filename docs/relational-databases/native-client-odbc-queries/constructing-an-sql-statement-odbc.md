---
title: Costruzione di un'istruzione SQL (ODBC) . Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
ms.assetid: 0acc71e2-8004-4dd8-8592-05c022bdd692
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eab0db859bbecea43d19b012a56b2e491b4ecfcf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291469"
---
# <a name="constructing-an-sql-statement-odbc"></a>Costruzione di un'istruzione SQL (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Le applicazioni ODBC eseguono l'accesso al database quasi sempre mediante l'esecuzione delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il formato di tali istruzioni dipende dai requisiti dell'applicazione. Le istruzioni SQL possono essere costruite nei modi seguenti:  
  
-   Hard-coded  
  
     Istruzioni statiche eseguite da un'applicazione come attività fissa.  
  
-   In fase di esecuzione  
  
     Istruzioni SQL costruite in fase di esecuzione che consentono all'utente di personalizzare l'istruzione servendosi di clausole comuni, ad esempio SELECT, WHERE e ORDER BY. Sono incluse query ad hoc immesse dagli utenti.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC client analizza le istruzioni SQL solo per le [!INCLUDE[ssDE](../../includes/ssde-md.md)]sintassi ODBC e [!INCLUDE[tsql](../../includes/tsql-md.md)]ISO non supportate direttamente dalla , che il driver trasforma in . Tutte le altre sintassi [!INCLUDE[ssDE](../../includes/ssde-md.md)] SQL vengono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] passate all'oggetto invariato, dove verrà determinato se è valido. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Questo approccio comporta due vantaggi:  
  
-   Riduzione dell'overhead  
  
     L'elaborazione dell'overhead per il driver viene ridotto al minimo, in quanto l'analisi deve essere eseguita solo per un piccolo set di clausole ODBC e ISO.  
  
-   Flessibilità  
  
     I programmatori possono personalizzare la portabilità delle applicazioni. Per migliorare la portabilità rispetto a più database, utilizzare principalmente la sintassi ODBC e ISO. Per utilizzare miglioramenti specifici di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilizzare la sintassi di [!INCLUDE[tsql](../../includes/tsql-md.md)] appropriata. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client [!INCLUDE[tsql](../../includes/tsql-md.md)] supporta la sintassi completa in modo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]che le applicazioni basate su ODBC possano sfruttare tutte le funzionalità di .  
  
 L'elenco di colonne di un'istruzione SELECT deve contenere solo le colonne richieste per eseguire l'attività corrente. In questo modo non solo si riduce la quantità di dati inviati attraverso la rete, ma anche l'effetto delle modifiche del database sull'applicazione. Se in un'applicazione non si fa riferimento a una colonna di una tabella, l'applicazione non viene interessata dalle modifiche apportate alla colonna.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di query &#40;&#41;ODBC](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
