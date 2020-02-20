---
title: Metodo getColumnPrivileges (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getColumnPrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ab6a671-9573-4b95-8c23-364306c60d25
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ae80a8c33f68ad2f3d2c85b1343a5cc0f2b423c5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67952870"
---
# <a name="getcolumnprivileges-method-sqlserverdatabasemetadata"></a>Metodo getColumnPrivileges (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione dei diritti di accesso per le colonne di una tabella.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getColumnPrivileges(java.lang.String catalog,  
                                              java.lang.String schema,  
                                              java.lang.String table,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parametri  
 *catalog*  
  
 Valore **String** contenente il nome del catalogo.  
  
 *schema*  
  
 Valore **String** contenente il nome dello schema.  
  
 *tabella*  
  
 Valore **String** contenente il nome della tabella.  
  
 *col*  
  
 Valore **String** contenente il modello del nome della colonna.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getColumnPrivileges viene specificato dal metodo getColumnPrivileges nell'interfaccia java.sql.DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getColumnPrivileges conterrà le informazioni seguenti:  
  
|Nome|Type|Descrizione|  
|----------|----------|-----------------|  
|TABLE_CAT|**Stringa**|Nome del catalogo.|  
|TABLE_SCHEM|**Stringa**|Nome dello schema della tabella.|  
|TABLE_NAME|**Stringa**|Il nome della tabella.|  
|COLUMN_NAME|**Stringa**|Nome della colonna.|  
|GRANTOR|**Stringa**|Oggetto che concede l'accesso.|  
|GRANTEE|**Stringa**|Oggetto a cui si concede l'accesso.|  
|PRIVILEGE|**Stringa**|Tipo di accesso concesso.|  
|IS_GRANTABLE|**Stringa**|Indica se l'utente autorizzato può concedere l'accesso agli altri utenti.|  
  
> [!NOTE]  
>  Per altre informazioni sui dati restituiti dal metodo getColumnPrivileges, vedere "sp_column_privileges (Transact-SQL)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare il metodo getColumnPrivileges per restituire i diritti di accesso per la colonna FirstName nella tabella Person.Contact del database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetColumnPrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getColumnPrivileges("AdventureWorks", "Person", "Contact", "FirstName");  
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
  
  
