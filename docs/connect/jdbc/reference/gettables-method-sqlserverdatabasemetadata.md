---
title: Metodo getTables (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a7514673-3457-4541-9560-28a8284ad9e3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8dfd7f14d6006f5a41a7cd2a9b0cae4933804fe
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979215"
---
# <a name="gettables-method-sqlserverdatabasemetadata"></a>Metodo getTables (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione delle tabelle disponibili nel modello di nome di catalogo, di schema o di tabella specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getTables(java.lang.String catalog,  
                                    java.lang.String schema,  
                                    java.lang.String table,  
                                    java.lang.String[] types)  
```  
  
#### <a name="parameters"></a>Parametri  
 *catalog*  
  
 Valore **String** contenente il nome del catalogo. Se si specifica Null per questo parametro, non è necessario utilizzare il nome del catalogo.  
  
 *schema*  
  
 Valore **String** contenente il modello del nome dello schema. Se si specifica Null per questo parametro, non è necessario utilizzare il nome dello schema.  
  
 *tableName*  
  
 Valore **String** contenente il modello del nome della tabella.  
  
 *types*  
  
 Matrice di stringhe contenente i tipi di tabelle da includere. Null indica che devono essere inclusi tutti i tipi di tabelle.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getTables viene specificato dal metodo getTables nell'interfaccia java.sql.DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getTables conterrà le informazioni seguenti:  
  
|Nome|Type|Descrizione|  
|----------|----------|-----------------|  
|TABLE_CAT|**Stringa**|Nome del database contenente la tabella specificata.|  
|TABLE_SCHEM|**Stringa**|Nome dello schema della tabella.|  
|TABLE_NAME|**Stringa**|Il nome della tabella.|  
|TABLE_TYPE|**Stringa**|Tipo di tabella.|  
|REMARKS|**Stringa**|Descrizione della tabella.<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non restituisce un valore per questa colonna.|  
|TYPE_CAT|**Stringa**|Non supportato dal driver JDBC.|  
|TYPE_SCHEM|**Stringa**|Non supportato dal driver JDBC.|  
|TYPE_NAME|**Stringa**|Non supportato dal driver JDBC.|  
|SELF_REFERENCING_COL_NAME|**Stringa**|Non supportato dal driver JDBC.|  
|REF_GENERATION|**Stringa**|Non supportato dal driver JDBC.|  
  
> [!NOTE]  
>  Per ulteriori informazioni sui dati restituiti dal metodo getTables, vedere "sp_tables (Transact-SQL)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare il metodo getTables per restituire le informazioni sulla descrizione della tabella Person.Contact del database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetTables(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTables("AdventureWorks", "Person", "Contact", null);  
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
  
  
