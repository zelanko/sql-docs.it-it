---
description: Metodo getSearchStringEscape (SQLServerDatabaseMetaData)
title: Metodo getSearchStringEscape (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSearchStringEscape
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea0f95d0-0238-4dc8-9f26-7ff9b65f30c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5801a6a971a0714af8408fa15c206770b9101bd5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434633"
---
# <a name="getsearchstringescape-method-sqlserverdatabasemetadata"></a>Metodo getSearchStringEscape (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore **String** che può essere usato come escape per i caratteri jolly.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getSearchStringEscape()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente la stringa di carattere jolly di escape.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getSearchStringEscape viene specificato dal metodo getSearchStringEscape nell'interfaccia java.sql.DatabaseMetaData.  
  
 Questo metodo viene utilizzato solo per le ricerche con criteri di metadati. Restituisce "\\". Un criterio di ricerca **String** può usare la sequenza di escape per i caratteri jolly ("%" e "_") e fornirli come valori letterali anteponendo una barra rovesciata. In questo modo, "\\%" viene convertito in "[%]" e "\\\_" viene convertito in "[\_]".  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
