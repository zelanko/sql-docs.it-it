---
title: Metodo getExportedKeys (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getExportedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 26888e61-b243-4a1b-922c-c0a451dcff4d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e89d65955c5637bcd566d48b6e54bcae50397d88
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983307"
---
# <a name="getexportedkeys-method-sqlserverdatabasemetadata"></a>Metodo getExportedKeys (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione delle colonne di chiave esterna che fanno riferimento alle colonne di chiave primaria della tabella specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getExportedKeys(java.lang.String cat,  
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
 Questo metodo getExportedKeys viene specificato dal metodo getExportedKeys nell'interfaccia java. SQL. DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getExportedKeys conterrà le informazioni seguenti:  
  
|nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**String**|Nome del catalogo che contiene la tabella di chiave primaria.|  
|PKTABLE_SCHEM|**String**|Nome dello schema della tabella di chiave primaria.|  
|PKTABLE_NAME|**String**|Nome della tabella di chiave primaria.|  
|PKCOLUMN_NAME|**String**|Nome della colonna della chiave primaria.|  
|FKTABLE_CAT|**String**|Nome del catalogo che contiene la tabella di chiave esterna.|  
|FKTABLE_SCHEM|**String**|Nome dello schema della tabella di chiave esterna.|  
|FKTABLE_NAME|**String**|Nome della tabella di chiave esterna.|  
|FKCOLUMN_NAME|**String**|Nome della colonna della chiave esterna.|  
|KEY_SEQ|**short**|Numero di sequenza della colonna in una chiave primaria a più colonne.|  
|UPDATE_RULE|**short**|Azione applicata alla chiave esterna quando l'operazione SQL è un aggiornamento. Può essere uno dei valori seguenti:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**short**|Azione applicata alla chiave esterna quando l'operazione SQL è un'eliminazione. Può essere uno dei valori seguenti:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**String**|Nome della chiave esterna.|  
|PK_NAME|**String**|Nome della chiave primaria.|  
|DEFERRABILITY|**short**|Indica se la valutazione del vincolo di chiave esterna può essere posticipata fino a quando non viene eseguito un commit. Può essere uno dei valori seguenti:<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  Per altre informazioni sui dati restituiti dal metodo getExportedKeys, vedere "sp_fkeys (Transact-SQL)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare il metodo getExportedKeys per restituire le informazioni su tutte le chiavi esterne che fanno riferimento alle chiavi primarie della tabella Person.Contact nel database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetExportedKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getExportedKeys("AdventureWorks", "Person", "Contact");  
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
  
  
