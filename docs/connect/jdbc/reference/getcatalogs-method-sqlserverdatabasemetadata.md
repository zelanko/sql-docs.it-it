---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7ad65c0563598b06b88d2d3f744ade4f37a8fc8
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2019
ms.locfileid: "58305949"
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
  
## <a name="remarks"></a>Remarks  
 Questo metodo getCatalogs viene specificato dal metodo getCatalogs nell'interfaccia java.sql.DatabaseMetaData.  
  
> [!NOTE]  
>  In SQL Azure, è necessario connettersi al database master per chiamare **SQLServerDatabaseMetaData.getCatalogs**. SQL Azure non supporta la restituzione dell'intero set di cataloghi da un database utente. **SQLServerDatabaseMetaData.getCatalogs** utilizza la vista sys. Databases per ottenere i cataloghi. Fare riferimento alla trattazione delle autorizzazioni in [Sys. database_usage (Database SQL di Azure)](../../../relational-databases/system-catalog-views/sys-database-usage-azure-sql-database.md) comprendere **SQLServerDatabaseMetaData.getCatalogs** comportamento in SQL Azure.  
  
 Il set di risultati restituito dal metodo getCatalogs conterrà le informazioni seguenti:  
  
|nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|Nome del catalogo, inclusi i database di sistema di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare il metodo getCatalogs per restituire i nomi di tutti i database contenuti in [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], inclusi i database di sistema.  
  
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
  
  
