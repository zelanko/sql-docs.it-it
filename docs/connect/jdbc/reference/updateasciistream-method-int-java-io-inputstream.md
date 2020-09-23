---
description: Metodo updateAsciiStream (int, java.io.InputStream)
title: updateAsciiStream method (int, java.io.InputStream)
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1dcc3d4f-ae30-45c0-afad-a531358807af
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c72fe46e637a37f33b9d9f89219eb71c4fb6b60a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462379"
---
# <a name="updateasciistream-method-int-javaioinputstream"></a>Metodo updateAsciiStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aggiorna la colonna designata con un valore del flusso ASCII.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void updateAsciiStream(int columnIndex,  
                              java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnIndex*  
  
 Valore **int** che indica l'indice di colonna.  
  
 *x*  
  
 Oggetto InputStream.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo updateAsciiStream viene specificato dal metodo updateAsciiStream nell'interfaccia java.sql.ResultSet.  
  
 Questo metodo passa caratteri ASCII (byte) da un oggetto InputStream a colonne di tipo carattere convertibili, ovvero l'intervallo ASCII [0x00 - 0x7F] di Unicode e le tabelle codici 874, 932, 936 949 e 950 e da 1250 a 1258. Esegue una conversione nella pagina delle regole di confronto di destinazione. Se si tenta di aggiornare una colonna di destinazione non convertibile, verrà generata un'eccezione. Per le colonne binarie, vengono passati byte non elaborati.  
  
 L'uso di questo metodo per i tipi di dati **image**, **text** e **ntext** di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può influire sulle prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo updateAsciiStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
