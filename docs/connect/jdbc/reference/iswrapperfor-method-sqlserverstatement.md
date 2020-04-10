---
title: Metodo isWrapperFor (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53f3291f-d43a-476b-a656-d86168dacf6c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e98b901663a63b353e14ae31308e244a55a78369
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80915125"
---
# <a name="iswrapperfor-method-sqlserverstatement"></a>Metodo isWrapperFor (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se questo oggetto istruzione è un wrapper per l'interfaccia specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Parametri  
 *iface*  
  
 Valore **class** che definisce un'interfaccia.  
  
## <a name="return-value"></a>Valore restituito  
 **true** se questo oggetto implementa l'interfaccia o esegue il wrapping di un oggetto che implementa l'interfaccia. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) e il metodo [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) sono definiti dall'interfaccia java.sql.Wrapper, introdotta in JDBC 4.0.  
  
 Se questo metodo restituisce true, la chiamata a [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) con lo stesso argomento avrà esito positivo.  
  
 Per un esempio di codice, vedere [Esempio di aggiornamento di dati di grandi dimensioni](../../../connect/jdbc/updating-large-data-sample.md).  
  
 Per altre informazioni, vedere [Wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo unwrap &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)   
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
