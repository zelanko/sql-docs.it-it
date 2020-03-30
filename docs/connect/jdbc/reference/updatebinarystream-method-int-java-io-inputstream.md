---
title: Metodo updateBinaryStream(int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1db3a975-c108-45d1-8c0d-14a094f391bd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a1b69d4f4e1845b4ec86297c06298c1302becea
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67985379"
---
# <a name="updatebinarystream-method-int-javaioinputstream"></a>Metodo updateBinaryStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aggiorna la colonna designata con un valore del flusso binario.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void updateBinaryStream(int columnIndex,  
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
 Questo metodo updateBinaryStream viene specificato dal metodo updateBinaryStream nell'interfaccia java.sql.ResultSet.  
  
 L'uso di questo metodo per i tipi di dati **image**, **text** e **ntext** di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può influire sulle prestazioni.  
  
 Questo metodo passa byte da un oggetto InputStream a colonne binarie di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] selezionate, ad esempio binary, varbinary, varbinary(max), image, xml e udt. L'aggiornamento delle colonne di tipo carattere non è supportato con questo metodo. Per aggiornare le colonne di tipo carattere con un InputStream, usare il metodo [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo updateBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
