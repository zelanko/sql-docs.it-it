---
title: Metodo getCatalogSeparator (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogSeparator
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0bbd6842-7210-432a-bef4-e15a63f5cc96
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4c9c73652c1c0b512c24e2d592323833390c7b0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953338"
---
# <a name="getcatalogseparator-method-sqlserverdatabasemetadata"></a>Metodo getCatalogSeparator (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore **String** usato dal database come separatore tra un nome di catalogo e un nome di tabella.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getCatalogSeparator()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente il separatore di catalogo.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getCatalogSeparator viene specificato dal metodo getCatalogSeparator nell'interfaccia java.sql.DatabaseMetaData.  
  
 Quando si usa [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] questo metodo restituisce un punto (".") come separatore di catalogo.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
