---
title: Metodo setFloat (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setFloat
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 26d861da-bb6a-4197-8b32-13dc7781c2bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ef88415db781721815be6de51c6b94303e59b07
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922301"
---
# <a name="setfloat-method-sqlservercallablestatement"></a>Metodo setFloat (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore **float** specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setFloat(java.lang.String sCol,  
                     float f)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Valore **String** contenente il nome del parametro.  
  
 *f*  
  
 Valore **float**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setFloat viene specificato dal metodo setFloat nell'interfaccia java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
