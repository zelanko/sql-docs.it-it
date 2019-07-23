---
title: Metodo updateCharacterStream (int, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4dddf885-0482-4776-8e9a-69f6c6270931
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b08a6574f16159e5eebb9a95af7483b2ce7b0c84
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996757"
---
# <a name="updatecharacterstream-method-int-javaioreader"></a>Metodo updateCharacterStream (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aggiorna la colonna designata con un valore del flusso di caratteri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnIndex*  
  
 Valore **int** che indica l'indice di colonna.  
  
 *x*  
  
 Oggetto Reader.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo updateCharacterStream viene specificato dal metodo updateCharacterStream nell'interfaccia java. SQL. ResultSet.  
  
 Questo metodo passa caratteri Unicode da un oggetto Reader alle colonne di testo e binarie selezionate. Include tutte le colonne di testo e le colonne **binary**, **varbinary**, **varbinary(max)** , **image** e **xml**, ma non le colonne **udt**.  
  
 L'utilizzo di questo metodo per i tipi di dati **Image**, **Text**e **ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può compromettere le prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo updateCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
