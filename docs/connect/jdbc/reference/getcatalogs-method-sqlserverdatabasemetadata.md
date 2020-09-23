---
description: Metodo getCatalogs (SQLServerDatabaseMetaData)
title: Metodo getCatalogs (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7f8bd0f1-f340-4bb9-b559-0a6176124033
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a31fca087c206104d197a3121db90991ff38f8c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436903"
---
# <a name="getcatalogs-method-sqlserverdatabasemetadata"></a>Metodo getCatalogs (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera i nomi di catalogo disponibili nel server connesso.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getCatalogs()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getCatalogs viene specificato dal metodo getCatalogs nell'interfaccia java.sql.DatabaseMetaData.  
  
> [!NOTE]  
>  Nel database SQL di Azure è necessario connettersi al database master per chiamare **SQLServerDatabaseMetaData.getCatalogs**. Il database SQL non supporta la restituzione dell'intero set di cataloghi da un database utente. **SQLServerDatabaseMetaData.getCatalogs** usa la vista sys.databases per ottenere i cataloghi. Per informazioni sul comportamento di **SQLServerDatabaseMetaData.getCatalogs** in SQL vedere la discussione sulle autorizzazioni in [sys.database_usage (Azure SQL Database)](../../../relational-databases/system-catalog-views/sys-database-usage-azure-sql-database.md) > Nel database SQL di Azure, collegarsi al database master per richiamare **SQLServerDatabaseMetaData.getCatalogs**. Il database SQL non supporta la restituzione dell'intero set di cataloghi da un database utente. **SQLServerDatabaseMetaData.getCatalogs** usa la vista sys.databases per ottenere i cataloghi. Per informazioni sul comportamento di **SQLServerDatabaseMetaData.getCatalogs** nel database SQL, vedere la discussione sulle autorizzazioni in [sys.database_usage (database SQL di Azure)](../../../relational-databases/system-catalog-views/sys-database-usage-azure-sql-database.md).                      .  
  
 Il set di risultati restituito dal metodo getCatalogs conterrà le informazioni seguenti:  
  
|Nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|TABLE_CAT|**Stringa**|Nome del catalogo, inclusi i database di sistema in [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
## <a name="example"></a>Esempio  
 L'esempio seguente dimostra come usare il metodo getCatalogs per restituire i nomi di tutti i database contenuti in [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], inclusi i database di sistema.  
  
```  
public static void executeGetCatalogs(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCatalogs();  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }   
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
