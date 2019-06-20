---
title: Metodo getProcedureColumns (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedureColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8c71218c709921cd9180bff2b9a6b5997ae7450c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66771200"
---
# <a name="getprocedurecolumns-method-sqlserverdatabasemetadata"></a>Metodo getProcedureColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione dei parametri delle stored procedure e delle colonne dei risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getProcedureColumns(java.lang.String sCatalog,  
                                              java.lang.String sSchema,  
                                              java.lang.String proc,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCatalog*  
  
 Valore **String** contenente il nome del catalogo. Se si specifica Null per questo parametro, non è necessario utilizzare il nome del catalogo.  
  
 *sSchema*  
  
 Valore **String** contenente il modello del nome dello schema. Se si specifica Null per questo parametro, non è necessario utilizzare il nome dello schema.  
  
 *proc*  
  
 Valore **String** contenente il modello del nome della procedura.  
  
 *col*  
  
 Valore **String** contenente il modello del nome della colonna. Se si specifica Null per questo parametro, viene restituita una riga per ogni colonna.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getProcedureColumns viene specificato dal metodo getProcedureColumns nell'interfaccia DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getProcedureColumns conterrà le informazioni seguenti:  
  
|nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|Nome del database in cui si trova la stored procedure specificata.|  
|PROCEDURE_SCHEM|**String**|Schema per la stored procedure.|  
|PROCEDURE_NAME|**String**|Nome della stored procedure.|  
|COLUMN_NAME|**String**|Nome della colonna.|  
|COLUMN_TYPE|**short**|Tipo di colonna. Può essere uno dei valori seguenti:<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**smallint**|Tipo di dati SQL da java.sql.Types.|  
|TYPE_NAME|**String**|Nome del tipo di dati.|  
|PRECISION|**int**|Numero totale di cifre significative.|  
|LENGTH|**int**|Lunghezza dei dati in byte.|  
|SCALE|**short**|Numero di cifre a destra del separatore decimale.|  
|RADIX|**short**|Base per i tipi numerici.|  
|NULLABLE|**short**|Indica se la colonna può contenere un valore Null. Può essere uno dei valori seguenti:<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|REMARKS|**String**|Descrizione della colonna della procedura.<br /><br /> <br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non restituisce un valore per questa colonna.|  
|COLUMN_DEF|**String**|Valore predefinito della colonna.|  
|SQL_DATA_TYPE|**smallint**|Questa colonna corrisponde alla colonna **DATA_TYPE**, tranne che per i tipi di dati **datetime** e ISO **interval**.|  
|SQL_DATETIME_SUB|**smallint**|Sottocodice **datetime** ISO **interval** se il valore di **SQL_DATA_TYPE** è **SQL_DATETIME** o **SQL_INTERVAL**. Per i dati di tipi diversi da **data/ora** e ISO **intervallo**, questa colonna è NULL.|  
|CHAR_OCTET_LENGTH|**int**|Numero massimo di byte nella colonna.|  
|ORDINAL_POSITION|**int**|Indice della colonna all'interno della tabella.|  
|IS_NULLABLE|**String**|Indica se la colonna ammette valori Null.|  
|SS_TYPE_CATALOG_NAME|**String**|Nome del catalogo contenente il tipo definito dall'utente (UDT).|  
|SS_TYPE_SCHEMA_NAME|**String**|Nome dello schema contenente il tipo definito dall'utente (UDT).|  
|SS_UDT_CATALOG_NAME|**String**|Tipo definito dall'utente (UDT) del nome completo.|  
|SS_UDT_SCHEMA_NAME|**String**|Nome del catalogo in cui viene definito il nome di una raccolta di XML Schema. Se non è possibile trovare il nome del catalogo, questa variabile contiene una stringa vuota.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|Nome dello schema in cui viene definito il nome di una raccolta di XML Schema. Se non è possibile trovare il nome dello schema, viene visualizzata una stringa vuota.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|Nome di una raccolta di XML Schema. Se non è possibile trovare il nome, viene visualizzata una stringa vuota.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|Nome del catalogo contenente il tipo definito dall'utente (UDT).|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|Nome dello schema contenente il tipo definito dall'utente (UDT).|  
|SS_DATA_TYPE|**tinyint**|Tipo di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usato in stored procedure estese.<br /><br /> <br /><br /> **Nota**: per altre informazioni sui tipi di dati restituiti da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere "Tipi di dati (Transact-SQL)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
> [!NOTE]  
>  Per altre informazioni sui dati restituiti dal metodo getProcedureColumns, vedere "sp_sproc_columns (Transact-SQL)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare il metodo getProcedureColumns per restituire informazioni sulla stored procedure uspGetBillOfMaterials nel database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetProcedureColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedureColumns(null, null, "uspGetBillOfMaterials", null);  
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
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
