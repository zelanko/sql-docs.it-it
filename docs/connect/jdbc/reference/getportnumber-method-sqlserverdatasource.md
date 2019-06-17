---
title: Metodo getPortNumber (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b731bf5ce8272fe72167d77b96e523cd3ede1139
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66771330"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>Metodo getPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il numero della porta corrente usata per comunicare con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** contenente il numero di porta corrente.  
  
## <a name="remarks"></a>Remarks  
 Il numero di porta è il numero di porta TCP/IP usato quando si apre una connessione socket a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se la proprietà portNumber non è impostata, il metodo getPortNumber restituisce il valore predefinito 1433.  
  
> [!NOTE]  
>  Il [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) metodo non esegue alcun controllo sul valore di porta passato di intervallo. È possibile passare numeri che non sono validi, come 99999, senza generare un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
