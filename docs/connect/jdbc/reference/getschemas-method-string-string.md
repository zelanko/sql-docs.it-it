---
description: Metodo getSchemas (String, String)
title: Metodo getSchemas (String, String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 672171ac-976f-4605-9bee-2a5e141d92cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a3b421ae475d6c161396380073d1d8336b7f1b26
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434643"
---
# <a name="getschemas-method-string-string"></a>Metodo getSchemas (String, String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera i nomi di schema disponibili nel database corrente tramite il nome di catalogo specificato e il nome dello schema.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public ResultSet getSchemas(java.lang.String catalog,  
                       java.lang.String schemaPattern)  
```  
  
#### <a name="parameters"></a>Parametri  
 *catalog*  
  
 Nome di un catalogo del database. Se è una stringa vuota (""), il risultato include gli schemi senza un catalogo. Se è **null**, il nome del catalogo non viene usato per la ricerca.  
  
 *schemaPattern*  
  
 Nome di uno schema. Se è **null**, il nome dello schema non viene usato per la ricerca.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getSchemas viene specificato dal metodo getSchemas nell'interfaccia java.sql.DatabaseMetaData.  
  
 Il set di risultati restituito dal metodo getSchemas contiene le informazioni riportate di seguito:  
  
|Nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**Stringa**|Nome dello schema.|  
|TABLE_CATALOG|**Stringa**|Nome di catalogo per lo schema.|  
  
 I risultati vengono ordinati in base a TABLE_CATALOG e quindi in base a TABLE_SCHEM. La prima colonna di ogni riga è TABLE_SCHEM, mentre la seconda è TABLE_CATALOG.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
