---
title: Metodo getUDTs (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getUDTs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c4396453-dcb0-4132-8325-06b3c7896b3b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 610218dd7b1439e5e032bfc0a8f53893f6894f32
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910997"
---
# <a name="getudts-method-sqlserverdatabasemetadata"></a>Metodo getUDTs (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione dei tipi definiti dall'utente configurati in un determinato schema.  
  
> [!NOTE]  
>  Questo metodo non è attualmente supportato con [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Quando viene utilizzato questo metodo, viene restituito sempre un set di risultati vuoto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.ResultSet getUDTs(java.lang.String catalog,  
                                  java.lang.String schemaPattern,  
                                  java.lang.String typeNamePattern,  
                                  int[] types)  
```  
  
#### <a name="parameters"></a>Parametri  
 *catalog*  
  
 Valore **String** contenente il nome del catalogo.  
  
 *schemaPattern*  
  
 Valore **String** contenente il modello del nome dello schema.  
  
 *typeNamePattern*  
  
 Valore **String** contenente il modello del nome del tipo.  
  
 *types*  
  
 Una matrice di valori ints contenente i tipi di dati da includere. Null indica che devono essere inclusi tutti i tipi.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getUDTs viene specificato dal metodo getUDTs nell'interfaccia java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
