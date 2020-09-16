---
description: Metodo getServerPreparedStatementDiscardThreshold (SQLServerDataSource)
title: Metodo getServerPreparedStatementDiscardThreshold (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e779955f77be3891bb3f7479b4a40fb30b3d56ac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434543"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>Metodo getServerPreparedStatementDiscardThreshold (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il valore della proprietà di connessione **serverPreparedStatementDiscardThreshold**. Questa impostazione consente di controllare il numero di azioni di annullamento di istruzioni preparate (sp_unprepare) in sospeso per ogni connessione prima che venga eseguita una chiamata per pulire gli handle in sospeso nel server. Quando l'impostazione è <= 1, le azioni di annullamento della preparazione vengono eseguite immediatamente alla chiusura dell'istruzione preparata. Se questo valore è impostato su > 1, queste chiamate vengono eseguite in batch per evitare il sovraccarico di chiamate troppo frequenti di sp_unprepare.

  
## <a name="syntax"></a>Sintassi  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce il valore **int** della proprietà di connessione **serverPreparedStatementDiscardThreshold**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Osservazioni  
 Questo metodo è disponibile dal driver JDBC versione 6.4 e successive.
 
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
