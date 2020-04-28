---
title: Utilizzo delle funzioni di catalogo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, functions
- SQLLinkedCatalogs function
- SQL Server Native Client ODBC driver, catalog functions
- SQLLinkedServers function
- catalog functions [ODBC]
- functions [ODBC]
ms.assetid: 7773fb2e-06b5-4c4b-88e9-0ad9132ad273
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 961e44e22ba7db89537f4505a8dec401f9fd69b0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303632"
---
# <a name="using-catalog-functions"></a>Utilizzo delle funzioni di catalogo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Tutti i database presentano una struttura che contiene i dati archiviati nel database. Una definizione di tale struttura, insieme ad altre informazioni quali le autorizzazioni, è archiviata in un catalogo (implementato come un set di tabelle di sistema), noto anche come dizionario dei dati.  
  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client consente a un'applicazione di determinare la struttura del database tramite chiamate alle funzioni di catalogo ODBC. Le funzioni di catalogo restituiscono informazioni nei set di risultati e vengono implementate utilizzando stored procedure di catalogo per eseguire query sulle tabelle di sistema nel catalogo. Un'applicazione potrebbe ad esempio richiedere un set di risultati contenente informazioni su tutte le tabelle del sistema o tutte le colonne di una particolare tabella. Le funzioni di catalogo ODBC standard vengono utilizzate per ottenere informazioni di catalogo dal computer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al quale è connessa l'applicazione.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta query distribuite grazie alle quali è possibile accedere con un'unica query ai dati provenienti da più origini dati OLE DB eterogenee. Uno dei metodi di accesso a un'origine dati OLE DB remota consiste nel definire l'origine dati come server collegato. A tale scopo, è possibile utilizzare [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Dopo che è stato definito il server collegato, è possibile fare riferimento agli a oggetti del server nelle istruzioni Transact-SQL utilizzando un nome costituito da quattro parti:  
  
 *linked_server_name. Catalog. Schema. object_name*.  
  
 Il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta due funzioni specifiche del driver per il recupero delle informazioni di catalogo dai server collegati:  
  
-   **SQLLinkedServers**  
  
     Restituisce un elenco dei server collegati definiti nel server locale.  
  
-   **SQLLinkedCatalogs**  
  
     Restituisce un elenco dei cataloghi presenti in un server collegato.  
  
 Quando si dispone di un nome di server collegato e di un nome [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di catalogo, il driver ODBC di Native Client supporta il recupero di informazioni dal catalogo utilizzando un nome in due parti _linked_server_name_**.** _Catalog_ per *CatalogName* nelle funzioni del catalogo ODBC seguenti:  
  
-   **SQLColumnPrivileges**  
  
-   **SQLColumns**  
  
-   **SQLPrimaryKeys**  
  
-   **SQLStatistics**  
  
-   **SQLTablePrivileges**  
  
-   **SQLTables**  
  
 Linked_server_name in due parti _linked_server_name_**.** il _Catalogo_ è supportato anche per *FKCatalogName* e *PKCatalogName* in [SQLForeignKeys](../../../relational-databases/native-client-odbc-api/sqlforeignkeys.md).  
  
 L'utilizzo di SQLLinkedServers e SQLLinkedCatalogs richiede i file seguenti:  
  
-   sqlncli.h  
  
     Include prototipi della funzione e definizioni costanti per le funzioni del catalogo del server collegato. sqlncli.h deve essere incluso nell'applicazione ODBC e deve trovarsi nel percorso di inclusione al momento della compilazione dell'applicazione.  
  
-   sqlncli11.lib  
  
     Deve trovarsi nel percorso della libreria del linker e deve essere specificato come un file da collegare. sqlncli11.lib è distribuito con il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   sqlncli11.dll  
  
     Deve essere presente in fase di esecuzione. sqlncli11.dll è distribuito con il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLColumnPrivileges](../../../relational-databases/native-client-odbc-api/sqlcolumnprivileges.md)   
 [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)   
 [SQLPrimaryKeys](../../../relational-databases/native-client-odbc-api/sqlprimarykeys.md)   
 [SQLTablePrivileges](../../../relational-databases/native-client-odbc-api/sqltableprivileges.md)   
 [SQLTables](../../../relational-databases/native-client-odbc-api/sqltables.md)   
 [SQLStatistics](../../../relational-databases/native-client-odbc-api/sqlstatistics.md)  
  
  
