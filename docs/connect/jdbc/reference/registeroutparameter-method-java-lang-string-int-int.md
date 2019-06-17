---
title: Metodo registerOutParameter per tipo e la scalabilità | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bddc557-4526-4843-9804-05dc83c8832d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 36f8300ade9c8b514f4c1efdee9848fafb8b5683
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802071"
---
# <a name="registeroutparameter-method-javalangstring-int-int"></a>Metodo registerOutParameter (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra il parametro OUT con il nome specificato nel tipo e nella scala JDBC forniti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void registerOutParameter(java.lang.String s,  
                                 int n,  
                                 int n1)  
```  
  
#### <a name="parameters"></a>Parametri  
 *s*  
  
 Valore **String** contenente il nome del parametro.  
  
 *sqlType*  
  
 Codice di tipo JDBC come definito in java.sql.Types.  
  
 *scala*  
  
 Valore **int** che indica il numero di cifre da posizionare a destra del separatore decimale.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo registerOutParameter viene specificato dal metodo registerOutParameter nell'interfaccia CallableStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo registerOutParameter &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
