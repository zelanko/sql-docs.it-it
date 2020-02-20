---
title: Metodo getIndexInfo (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8dd512236aa3070ce299756d4e4294c79ac2e94a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982796"
---
# <a name="getindexinfo-method-sqlserverdatabasemetadata"></a>Metodo getIndexInfo (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione degli indici e delle statistiche per la tabella specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getIndexInfo(java.lang.String cat,  
                                       java.lang.String schema,  
                                       java.lang.String table,  
                                       boolean unique,  
                                       boolean approximate)  
```  
  
#### <a name="parameters"></a>Parametri  
 *cat*  
  
 Valore **String** contenente il nome del catalogo.  
  
 *schema*  
  
 Valore **String** contenente il nome dello schema.  
  
 *tabella*  
  
 Valore **String** contenente il nome della tabella.  
  
 *unique*  
  
 **true** se vengono restituiti solo gli indici per i valori univoci. **false** se vengono restituiti tutti gli indici.  
  
 *approximate*  
  
 **true** se i risultati riflettono valori approssimativi o non aggiornati. **false** se i risultati sono accurati.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getIndexInfo viene specificato dal metodo getIndexInfo nell'interfaccia java.sql.DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getIndexInfo conterrà le informazioni seguenti:  
  
|Nome|Type|Descrizione|  
|----------|----------|-----------------|  
|TABLE_CAT|**Stringa**|Nome del database contenente la tabella specificata.|  
|TABLE_SCHEM|**Stringa**|Schema della tabella.|  
|TABLE_NAME|**Stringa**|Nome della tabella.|  
|NON_UNIQUE|**boolean**|Indica se i valori di indice possono essere non univoci.|  
|INDEX_QUALIFIER|**Stringa**|Nome del proprietario dell'indice. Sarà Null se TYPE è tableIndexStatistic.|  
|INDEX_NAME|**Stringa**|Nome dell'indice.|  
|TYPE|**short**|Tipo dell'indice. Può essere uno dei valori seguenti:<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**short**|Posizione ordinale della colonna nell'indice. La prima colonna nell'indice è 1.|  
|COLUMN_NAME|**Stringa**|Nome della colonna.|  
|ASC_OR_DESC|**Stringa**|Ordine utilizzato nelle regole di confronto dell'indice. Può essere uno dei valori seguenti:<br /><br /> A (crescente)<br /><br /> D (decrescente)<br /><br /> NULL (non applicabile)<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] restituisce sempre "A".|  
|CARDINALITY|**int**|Numero di righe nella tabella o di valori univoci nell'indice.|  
|PAGES|**int**|Numero di pagine utilizzate per l'archiviazione dell'indice o della tabella.|  
|FILTER_CONDITION|**Stringa**|Condizione di filtro.<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] restituisce sempre Null.|  
  
> [!NOTE]  
>  Per altre informazioni sui dati restituiti dal metodo getIndexInfo, vedere "sp_indexes (Transact-SQL)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare il metodo getIndexInfo per restituire le informazioni sugli indici e sulle statistiche della tabella Person.Contact del database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetIndexInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getIndexInfo("AdventureWorks", "Person", "Contact", false, true);  
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
  
  
