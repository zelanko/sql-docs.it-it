---
title: Metodo getURL (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fcb66851-db5f-4ae8-b728-d129480b6f42
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f170e15ec0096d02fd98acb16e15a6ac05257f31
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779741"
---
# <a name="geturl-method-sqlserverdatabasemetadata"></a>Metodo getURL (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera l'URL del database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** che contiene l'URL.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getURL viene specificato dal metodo getURL nell'interfaccia java.sql.DatabaseMetaData.  
  
 Quando si usa [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con un database [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], questo metodo restituisce un valore **String** contenente le informazioni seguenti:  
  
-   Un valore URL di "jdbc:sqlserver://"  
  
-   Proprietà di connessione facoltative, ad esempio **serverName**, **instanceName**, e **NumeroPorta**  
  
-   Altre proprietà di connessione impostate dall'utente e tutte le proprietà di connessione con i valori predefiniti del driver non vuoti o non Null eccetto **userName**, **password** e **integratedSecurity**.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
