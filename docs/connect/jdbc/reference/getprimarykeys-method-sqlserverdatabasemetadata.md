---
title: Metodo getPrimaryKeys (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getPrimaryKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebfe236a-dc02-493e-a3ab-5353d3769e36
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bdb1eb0053c9bb15c6d03013df13635e022a5072
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980760"
---
# <a name="getprimarykeys-method-sqlserverdatabasemetadata"></a>Metodo getPrimaryKeys (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione delle colonne di chiave primaria della tabella specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getPrimaryKeys(java.lang.String cat,  
                                         java.lang.String schema,  
                                         java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parametri  
 *cat*  
  
 Valore **String** contenente il nome del catalogo.  
  
 *schema*  
  
 Valore **String** contenente il nome dello schema.  
  
 *table*  
  
 Valore **String** contenente il nome della tabella.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getPrimaryKeys viene specificato dal metodo getPrimaryKeys nell'interfaccia java. SQL. DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getPrimaryKeys conterrà le informazioni seguenti:  
  
|nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|TABLE_CAT|String|Nome del database contenente la tabella specificata.|  
|TABLE_SCHEM|String|Schema della tabella.|  
|TABLE_NAME|String|Nome della tabella.|  
|COLUMN_NAME|String|Nome della colonna.|  
|KEY_SEQ|short|Numero di sequenza della colonna in una chiave primaria a più colonne.|  
|PK_NAME|String|Nome della chiave primaria.|  
  
> [!NOTE]  
>  Per altre informazioni sui dati restituiti dal metodo getPrimaryKeys, vedere "sp_pkeys (Transact-SQL)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare il metodo getPrimaryKeys per restituire le informazioni sulle chiavi primarie della tabella Person.Contact del database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetPrimaryKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getPrimaryKeys("AdventureWorks", "Person", "Contact");  
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
  
  
