---
title: Metodo getAsciiStream (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ff1d47e4-572a-4169-a631-ac261f7642b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22177442dcec9fb873d4a824b73845ce6fc9bfdf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67954125"
---
# <a name="getasciistream-method-sqlservernclob"></a>Metodo getAsciiStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore **NCLOB** designato dall'oggetto **NClob** come flusso ASCII.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.InputStream getAsciiStream()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto InputStream contenente i dati NCLOB.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getAsciiStream viene specificato dal metodo getAsciiStream nell'interfaccia java.sql.SQLServerNClob.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membri di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
