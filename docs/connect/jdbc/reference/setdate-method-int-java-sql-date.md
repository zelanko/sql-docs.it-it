---
title: Metodo setDate al valore di data - int | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setDate (int, java.sql.Date)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 12e5a4cc-45a2-4779-bbfc-e4da66829588
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cf86e81c3512ef29cc661388ec02ff204548fcac
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66793960"
---
# <a name="setdate-method-int-javasqldate"></a>Metodo setDate (int, java.sql.Date)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore di data specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setDate(int n,  
                          java.sql.Date x)  
```  
  
#### <a name="parameters"></a>Parametri  
 *n*  
  
 Valore **int** che indica il numero di parametro.  
  
 *x*  
  
 Un oggetto Data.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setDate viene specificato dal metodo setDate nell'interfaccia java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setDate &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)   
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
