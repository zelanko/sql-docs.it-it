---
title: Metodo getEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 37ae73434db2e2cd523a7a68a00a54d464867bff
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767204"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>Metodo getEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il valore del **enablePrepareOnFirstPreparedStatementCall** proprietà di connessione. Se questa configurazione restituisce false la prima esecuzione di un'istruzione preparata chiamerà sp_executesql e non prepara un'istruzione, una volta che si verifica la seconda esecuzione chiamerà sp_prepexec ed effettivamente impostare un handle di istruzione preparata. Esecuzioni seguito chiamerà sp_execute. Ciò riduce la necessità per sp_unprepare in istruzione preparata chiudere se l'istruzione viene eseguita solo una volta. 
  
## <a name="syntax"></a>Sintassi  
  
```
public boolean getEnablePrepareOnFirstPreparedStatementCall();  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce il **booleana** pari al **enablePrepareOnFirstPreparedStatementCall** proprietà di connessione.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e progressiva.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
