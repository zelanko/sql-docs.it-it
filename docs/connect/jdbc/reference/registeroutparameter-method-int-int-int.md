---
title: Metodo registerOutParameter (int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d902d4e0-881f-4182-814c-0ede9a8da7fd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: df9265a677d9e44c2d8834d3c45525b7af80142a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802111"
---
# <a name="registeroutparameter-method-int-int-int"></a>Metodo registerOutParameter (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra il parametro OUT nella posizione ordinale specificata nel tipo e nella scala JDBC specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType,  
                                 int scale)  
```  
  
#### <a name="parameters"></a>Parametri  
 *index*  
  
 Valore **int** che indica la posizione ordinale del parametro.  
  
 *sqlType*  
  
 Codice di tipo JDBC come definito in java.sql.Types.  
  
 *scala*  
  
 Valore **int** che indica il numero di cifre da posizionare a destra del separatore decimale.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo registerOutParameter viene specificato dal metodo registerOutParameter nell'interfaccia CallableStatement.  
  
 A partire [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0, quando *sqlType* è di Types. Time tipo, il comportamento di questo metodo viene modificato dal **sendTimeAsDatetime** proprietà di connessione ([Impostando le proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md)) e [Setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Per altre informazioni, vedere [Java configurazione come valori vengono inviati al Server](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo registerOutParameter &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
