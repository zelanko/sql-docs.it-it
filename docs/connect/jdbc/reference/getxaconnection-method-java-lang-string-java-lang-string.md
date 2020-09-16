---
description: Metodo getXAConnection (java.lang.String, java.lang.String)
title: Metodo getXAConnection (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXADataSource.getXAConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276e0093-3d42-4f73-acc4-2b5b98245b40
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 988c8c3d7c1ba3cc09d20ae35f066d260cf543fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433753"
---
# <a name="getxaconnection-method-javalangstring-javalangstring"></a>Metodo getXAConnection (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tenta di stabilire una connessione di database fisica utilizzando il nome utente e la password specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public javax.sql.XAConnection getXAConnection(java.lang.String user,  
                                              java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parametri  
 *user*  
  
 Valore **String** contenente il nome utente.  
  
 *password*  
  
 Valore **String** che contiene la password.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto XAConnection.  
  
## <a name="exceptions"></a>Eccezioni  
 java.sql.SQLException  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getXAConnection viene specificato dal metodo getXAConnection nell'interfaccia javax.sql.XADataSource.  
  
> [!NOTE]  
>  Questo metodo viene in genere chiamato dalle implementazioni del pool di connessioni XA e non dal normale codice dell'applicazione JDBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getXAConnection &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [Metodi di SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Membri di SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Classe SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
