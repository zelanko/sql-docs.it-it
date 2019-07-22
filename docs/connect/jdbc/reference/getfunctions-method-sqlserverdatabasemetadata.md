---
title: Metodo GetFunctions (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b799fb56207294041c52fe455ad2acceff508d3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982949"
---
# <a name="getfunctions-method-sqlserverdatabasemetadata"></a>Metodo getFunctions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descrizione delle funzioni utente e di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public ResultSet getFunctions(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern)  
```  
  
#### <a name="parameters"></a>Parametri  
 *catalog*  
  
 Nome di un catalogo del database. Se è una stringa vuota (""), il risultato include le funzioni senza un catalogo. Se è **null**, il nome del catalogo non viene usato per la ricerca.  
  
 *schemaPattern*  
  
 Nome di uno schema. Se è una stringa vuota (""), il risultato include le funzioni senza uno schema. Se è **null**, il nome dello schema non viene usato per la ricerca.  
  
 *functionNamePattern*  
  
 Nome di una funzione.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getFunctions viene specificato dal metodo getFunctions nell'interfaccia java.sql.DatabaseMetaData.  
  
 Restituisce solo le funzioni utente e di sistema che corrispondono ai nomi di schema e funzione specificati.  
  
> [!IMPORTANT]  
>  Il set di risultati restituito può contenere funzioni per le quali l'utente chiamante non dispone delle autorizzazioni di esecuzione.  
  
 La descrizione di ogni funzione include le colonne seguenti:  
  
|nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|Nome del database contenente la funzione.|  
|FUNCTION_SCHEM|**String**|Nome dello schema contenente la funzione.|  
|FUNCTION_NAME|**String**|Nome della funzione.|  
|NUM_INPUT_PARAMS|**int**|Riservato per utilizzi futuri, attualmente restituisce un valore pari a -1.|  
|NUM_OUTPUT_PARAMS|**int**|Riservato per utilizzi futuri, attualmente restituisce un valore pari a -1.|  
|NUM_RESULT_SETS|**int**|Riservato per utilizzi futuri, attualmente restituisce un valore pari a -1.|  
|REMARKS|**String**|Commenti sulla funzione.|  
|FUNCTION_TYPE|**short**|Tipo della funzione. Può essere uno dei valori seguenti:<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
 Tutte le descrizioni del set di risultati restituito sono ordinate in base a FUNCTION_CAT, FUNCTION_SCHEM, FUNCTION_NAME e SPECIFIC_NAME.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
