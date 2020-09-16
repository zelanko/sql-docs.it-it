---
description: Metodo setAsciiStream (SQLServerNClob)
title: Metodo setAsciiStream (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 617ece92-0fb1-4f95-b32d-29b5b56eb3fb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20bed6696e28abdc57ec420c5b728a4978ddb44c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432554"
---
# <a name="setasciistream-method-sqlservernclob"></a>Metodo setAsciiStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un flusso da usare per scrivere caratteri ASCII nel valore **NCLOB** rappresentato da questo oggetto **java.sql.NClob**, a partire dalla posizione specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>Parametri  
 *pos*  
  
 Posizione di inizio della scrittura nell'oggetto **NCLOB**. La prima posizione è 1.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto OutputStream che rappresenta il flusso in cui possono essere scritti i caratteri ASCII.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setAsciiStream viene specificato dal metodo setAsciiStream nell'interfaccia java.sql.NClob.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membri di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
