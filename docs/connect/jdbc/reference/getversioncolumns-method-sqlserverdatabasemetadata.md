---
title: Metodo getVersionColumns (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getVersionColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6dd275d3-d9b2-4db7-938a-d4406c940a7a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8c098106fc3961e0248d638356df70527739203b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66780001"
---
# <a name="getversioncolumns-method-sqlserverdatabasemetadata"></a>Metodo getVersionColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione delle colonne di una tabella che viene aggiornata automaticamente all'aggiornamento di un valore di una riga.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getVersionColumns(java.lang.String catalog,  
                                            java.lang.String schema,  
                                            java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parametri  
 *catalog*  
  
 Valore **String** contenente il nome del catalogo.  
  
 *schema*  
  
 Valore **String** contenente il modello del nome dello schema.  
  
 *table*  
  
 Valore **String** contenente il nome della tabella.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getVersionColumns viene specificato dal metodo getVersionColumns nell'interfaccia java.sql.DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getVersionColumns conterrà le informazioni seguenti:  
  
|nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|SCOPE|**short**|Non supportato dal driver JDBC.|  
|COLUMN_NAME|**String**|Nome della colonna.|  
|DATA_TYPE|**short**|Tipo di dati SQL da java.sql.Types.|  
|TYPE_NAME|**String**|Nome del tipo di dati.|  
|COLUMN_SIZE|**int**|Precisione della colonna.|  
|BUFFER_LENGTH|**int**|Lunghezza della colonna in byte.|  
|DECIMAL_DIGITS|**short**|Scala della colonna.|  
|PSEUDO_COLUMN|**short**|Indica se la colonna è una pseudocolonna. Può essere uno dei valori seguenti:<br /><br /> versionColumnUnknown (0)<br /><br /> versionColumnNotPseudo (1)<br /><br /> versionColumnPseudo (2)|  
  
> [!NOTE]  
>  Per altre informazioni sui dati restituiti dal metodo getVersionColumns, vedere "sp_datatype_info (Transact-SQL)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare il metodo getVersionColumns per restituire le informazioni sulle colonne aggiornate automaticamente nella tabella Person.Contact del database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetVersionColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getVersionColumns("AdventureWorks", "Person", "Contact");  
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
  
  
