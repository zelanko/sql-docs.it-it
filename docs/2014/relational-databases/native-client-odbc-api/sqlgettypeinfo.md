---
title: SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4237ebcc22318fdd6a93af09a79d7f8e2bea8989
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705999"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client segnala la colonna aggiuntiva USERTYPE nel set di risultati di `SQLGetTypeInfo` . USERTYPE riporta la definizione del tipo di dati DB-Library e risulta utile agli sviluppatori che trasferiscono applicazioni DB-Library esistenti a ODBC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tratta l'identità come attributo, mentre ODBC la tratta come tipo di dati. Per risolvere questa mancata corrispondenza, `SQLGetTypeInfo` restituisce i tipi di dati: **intidentity**, **smallintidentity**, **TinyIntIdentity**, **decimalidentity**e **NumericIdentity**. La `SQLGetTypeInfo` colonna del set di risultati AUTO_UNIQUE_VALUE restituisce il valore true per questi tipi di dati.  
  
 Per **varchar**, **nvarchar** e **varbinary**, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client continua a segnalare rispettivamente 8000, 4000 e 8000 per il valore COLUMN_SIZE, anche se è effettivamente illimitato. Ciò consente di assicurare la compatibilità con le versioni precedenti.  
  
 Per il tipo di dati **XML** , il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client segnala SQL_SS_LENGTH_UNLIMITED per COLUMN_SIZE per indicare dimensioni illimitate.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo e parametri con valori di tabella  
 Il tipo di tabella per i parametri con valori di tabella è effettivamente un metatipo, ovvero un tipo usato per definire altri tipi. Non è pertanto necessario che venga esposta tramite SQLGetTypeInfo. Per recuperare i metadati per i tipi di tabella utilizzati con i parametri con valori di tabella, le applicazioni devono utilizzare SQLTables anziché SQLGetTypeInfo.  
  
 Per ulteriori informazioni sul recupero di metadati per i parametri con valori di tabella, vedere [attributi dell'istruzione che influiscono sui parametri con valori di tabella](../native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>Supporto di SQLGetTypeInfo per le caratteristiche avanzate di data e ora  
 Per i valori restituiti per i tipi data/ora, vedere [metadati del catalogo](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Per informazioni più generali, vedere [miglioramenti di data e ora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Supporto SQLGetTypeInfo per i tipi CLR definiti dall'utente di grandi dimensioni  
 `SQLGetTypeInfo` supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per ulteriori informazioni, vedere [tipi CLR definiti dall'utente di grandi dimensioni &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLGetTypeInfo (funzione)](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
