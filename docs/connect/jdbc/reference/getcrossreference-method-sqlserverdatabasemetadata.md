---
title: Metodo getCrossReference (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCrossReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 099dd0bf-b017-479d-9696-f5b06f4c6bf9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2fc70ed3e449840793dbd32e4d2014031256f3bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66763010"
---
# <a name="getcrossreference-method-sqlserverdatabasemetadata"></a>Metodo getCrossReference (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione delle colonne di chiave esterna per la tabella di chiave esterna specificata che fa riferimento alle colonne di chiave primaria della tabella di chiave primaria specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getCrossReference(java.lang.String cat1,  
                                            java.lang.String schem1,  
                                            java.lang.String tab1,  
                                            java.lang.String cat2,  
                                            java.lang.String schem2,  
                                            java.lang.String tab2)  
```  
  
#### <a name="parameters"></a>Parametri  
 *cat1*  
  
 Valore **String** contenente il nome del catalogo della tabella che contiene la chiave primaria.  
  
 *schem1*  
  
 Valore **String** contenente il nome dello schema della tabella che contiene la chiave primaria.  
  
 *tab1*  
  
 Valore **String** contenente il nome tabella della tabella che contiene la chiave primaria.  
  
 *cat2*  
  
 Valore **String** contenente il nome del catalogo della tabella che contiene la chiave esterna.  
  
 *schem2*  
  
 Valore **String** contenente il nome dello schema della tabella che contiene la chiave esterna.  
  
 *tab2*  
  
 Valore **String** contenente il nome tabella della tabella che contiene la chiave esterna.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getCrossReference viene specificato dal metodo getCrossReference nell'interfaccia DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getCrossReference conterrà le informazioni seguenti:  
  
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
>  Per altre informazioni sui dati restituiti dal metodo getCrossReference, vedere "sp_fkeys (Transact-SQL)" nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare il metodo getCrossReference per restituire informazioni sulle relazioni delle chiavi primaria ed esterna tra le tabelle Person.Contact e HumanResources.Employee del database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetCrossReference(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCrossReference("AdventureWorks", "Person", "Contact", null, "HumanResources", "Employee");  
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
  
  
