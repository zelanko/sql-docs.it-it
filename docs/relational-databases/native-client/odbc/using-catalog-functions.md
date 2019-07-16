---
title: Uso delle funzioni catalogo | Documenti di Microsoft
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c24e98f15793820df59bf372a73e42204814fb19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913076"
---
# <a name="using-catalog-functions"></a>Utilizzo delle funzioni di catalogo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Tutti i database presentano una struttura che contiene i dati archiviati nel database. Una definizione di tale struttura, insieme ad altre informazioni quali le autorizzazioni, è archiviata in un catalogo (implementato come un set di tabelle di sistema), noto anche come dizionario dei dati.  
  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client consente a un'applicazione determinare la struttura del database tramite chiamate alle funzioni di catalogo ODBC. Le funzioni di catalogo restituiscono informazioni nei set di risultati e vengono implementate utilizzando stored procedure di catalogo per eseguire query sulle tabelle di sistema nel catalogo. Un'applicazione potrebbe ad esempio richiedere un set di risultati contenente informazioni su tutte le tabelle del sistema o tutte le colonne di una particolare tabella. Le funzioni di catalogo ODBC standard vengono utilizzate per ottenere informazioni di catalogo dal computer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al quale è connessa l'applicazione.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta query distribuite grazie alle quali è possibile accedere con un'unica query ai dati provenienti da più origini dati OLE DB eterogenee. Uno dei metodi di accesso a un'origine dati OLE DB remota consiste nel definire l'origine dati come server collegato. Questa operazione può essere eseguita tramite [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Dopo che è stato definito il server collegato, è possibile fare riferimento agli a oggetti del server nelle istruzioni Transact-SQL utilizzando un nome costituito da quattro parti:  
  
 *linked_server_name.catalog.schema.object_name*.  
  
 Il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta due funzioni specifiche del driver per il recupero delle informazioni di catalogo dai server collegati:  
  
-   **SQLLinkedServers**  
  
     Restituisce un elenco dei server collegati definiti nel server locale.  
  
-   **SQLLinkedCatalogs**  
  
     Restituisce un elenco dei cataloghi presenti in un server collegato.  
  
 Dopo aver ottenuto un nome del server collegato e un nome di catalogo, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta recupero delle informazioni dal catalogo usando un nome composto due parti _linked_server_name_ **.** _catalog_ per *CatalogName* funzioni di catalogo in ODBC seguenti:  
  
-   **SQLColumnPrivileges**  
  
-   **SQLColumns**  
  
-   **SQLPrimaryKeys**  
  
-   **SQLStatistics**  
  
-   **SQLTablePrivileges**  
  
-   **SQLTables**  
  
 Le due parti _linked_server_name_ **.** _catalog_ è supportato anche per *FKCatalogName* e *PKCatalogName* sul [SQLForeignKeys](../../../relational-databases/native-client-odbc-api/sqlforeignkeys.md).  
  
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
  
  
