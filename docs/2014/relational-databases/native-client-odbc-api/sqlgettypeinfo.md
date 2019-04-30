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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60c4c4d364f9c07e9ca241dd357535f7f7acb42d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046694"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] report driver ODBC di Native Client imposta la colonna aggiuntiva USERTYPE nel risultato di `SQLGetTypeInfo`. USERTYPE riporta la definizione del tipo di dati DB-Library e risulta utile agli sviluppatori che trasferiscono applicazioni DB-Library esistenti a ODBC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tratta l'identità come attributo, mentre ODBC la tratta come tipo di dati. Per risolvere questa mancata corrispondenza, `SQLGetTypeInfo` restituisce i tipi di dati: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity** , e **numericidentity**. Il `SQLGetTypeInfo` colonna AUTO_UNIQUE_VALUE del set di risultati indica il valore TRUE per questi tipi di dati.  
  
 Per la **varchar**, **nvarchar** e **varbinary**, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client continua a segnalare 8000, 4000 e 8000 rispettivamente per il valore di COLUMN_SIZE il valore, anche se non esiste effettivamente alcun limite. Ciò consente di assicurare la compatibilità con le versioni precedenti.  
  
 Per il **xml** tipo di dati, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client riporta SQL_SS_LENGTH_UNLIMITED per COLUMN_SIZE indicare dimensioni illimitate.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo e parametri con valori di tabella  
 Il tipo di tabella per i parametri con valori di tabella è effettivamente un meta-tipo-che è, un tipo usato per definire altri tipi. Pertanto, è privo di essere esposti mediante SQLGetTypeInfo. Le applicazioni devono usare SQLTables, anziché SQLGetTypeInfo, per recuperare i metadati per i tipi di tabella utilizzati con i parametri con valori di tabella.  
  
 Per altre informazioni sul recupero di metadati per parametri con valori di tabella, vedere [gli attributi delle istruzioni che per i parametri Affect Table-Valued](../native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Per altre informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>Supporto di SQLGetTypeInfo per le caratteristiche avanzate di data e ora  
 Per i valori restituiti per i tipi data/ora, vedere [metadati del catalogo](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Per altre informazioni generali, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Supporto SQLGetTypeInfo per i tipi CLR definiti dall'utente di grandi dimensioni  
 `SQLGetTypeInfo` supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per altre informazioni, vedere [Large CLR User-Defined tipi &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLGetTypeInfo](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
