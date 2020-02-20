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
ms.openlocfilehash: f23da4d83217fbed39e6dddacfe92541eae0db23
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67984223"
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
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getCrossReference viene specificato dal metodo getCrossReference nell'interfaccia java.sql.DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getCrossReference conterrà le informazioni seguenti:  
  
|Nome|Type|Descrizione|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**Stringa**|Nome del catalogo che contiene la tabella di chiave primaria.|  
|PKTABLE_SCHEM|**Stringa**|Nome dello schema della tabella di chiave primaria.|  
|PKTABLE_NAME|**Stringa**|Nome della tabella di chiave primaria.|  
|PKCOLUMN_NAME|**Stringa**|Nome della colonna della chiave primaria.|  
|FKTABLE_CAT|**Stringa**|Nome del catalogo che contiene la tabella di chiave esterna.|  
|FKTABLE_SCHEM|**Stringa**|Nome dello schema della tabella di chiave esterna.|  
|FKTABLE_NAME|**Stringa**|Nome della tabella di chiave esterna.|  
|FKCOLUMN_NAME|**Stringa**|Nome della colonna della chiave esterna.|  
|KEY_SEQ|**short**|Numero di sequenza della colonna in una chiave primaria a più colonne.|  
|UPDATE_RULE|**short**|Azione applicata alla chiave esterna quando l'operazione SQL è un aggiornamento. Può essere uno dei valori seguenti:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**short**|Azione applicata alla chiave esterna quando l'operazione SQL è un'eliminazione. Può essere uno dei valori seguenti:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**Stringa**|Nome della chiave esterna.|  
|PK_NAME|**Stringa**|Nome della chiave primaria.|  
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
  
  
