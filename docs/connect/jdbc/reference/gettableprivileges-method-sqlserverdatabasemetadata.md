---
title: Metodo getTablePrivileges (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTablePrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0610d667-a16d-4201-a14b-0a40048911e1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d0fe3b01fd02bf48fb5f38707530e3b3344133e6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979226"
---
# <a name="gettableprivileges-method-sqlserverdatabasemetadata"></a>Metodo getTablePrivileges (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione dei diritti di accesso di ogni tabella disponibile nel modello di nome di catalogo, di schema o di tabella specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getTablePrivileges(java.lang.String catalog,  
                                             java.lang.String schema,  
                                             java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parametri  
 *catalog*  
  
 Valore **String** contenente il nome del catalogo. Se si specifica Null per questo parametro, non è necessario utilizzare il nome del catalogo.  
  
 *schema*  
  
 Valore **String** contenente il modello del nome dello schema. Se si specifica Null per questo parametro, non è necessario utilizzare il nome dello schema.  
  
 *tabella*  
  
 Valore **String** contenente il modello del nome della tabella.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getTablePrivileges viene specificato dal metodo getTablePrivileges nell'interfaccia java.sql.DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getTablePrivileges conterrà le informazioni seguenti:  
  
|Nome|Type|Descrizione|  
|----------|----------|-----------------|  
|TABLE_CAT|**Stringa**|Nome del catalogo.|  
|TABLE_SCHEM|**Stringa**|Nome dello schema della tabella.|  
|TABLE_NAME|**Stringa**|Il nome della tabella.|  
|GRANTOR|**Stringa**|Oggetto che concede l'accesso.|  
|GRANTEE|**Stringa**|Oggetto a cui si concede l'accesso.|  
|PRIVILEGE|**Stringa**|Tipo di accesso concesso.|  
|IS_GRANTABLE|**Stringa**|Indica se l'utente autorizzato può concedere l'accesso agli altri utenti.|  
  
> [!NOTE]  
>  Per ulteriori informazioni sui dati restituiti dal metodo getTablePrivileges, vedere "sp_table_privileges (Transact-SQL)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare il metodo getTablePrivileges per restituire i diritti di accesso per la tabella Person.Contact del database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetTablePrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTablePrivileges("AdventureWorks", "Person", "Contact");  
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
  
  
