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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2639e3c886f04e6284b04055492674ade6ba90a8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928122"
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
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo updateCharacterStream viene specificato dal metodo updateCharacterStream nell'interfaccia java.sql.ResultSet.  
  
 Questo metodo passa caratteri Unicode da un oggetto Reader alle colonne di testo e binarie selezionate. Include tutte le colonne di testo e le colonne **binary**, **varbinary**, **varbinary(max)** , **image** e **xml**, ma non le colonne **udt**.  
  
 L'uso di questo metodo per i tipi di dati **image**, **text** e **ntext** di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può influire sulle prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo updateCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
