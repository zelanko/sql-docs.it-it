---
title: SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ebeffb57ccfb6b651dc126f814615322250cd47e
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786321"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client riporta la colonna aggiuntiva USERTYPE nel set di risultati di **SQLGetTypeInfo**. USERTYPE riporta la definizione del tipo di dati DB-Library e risulta utile agli sviluppatori che trasferiscono applicazioni DB-Library esistenti a ODBC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tratta l'identità come attributo, mentre ODBC la tratta come tipo di dati. Per risolvere questa mancata corrispondenza, **SQLGetTypeInfo** restituisce i tipi di dati: **intidentity**, **smallintidentity**, **TinyIntIdentity**, **decimalidentity**e **NumericIdentity**. La colonna del set di risultati **SQLGetTypeInfo** AUTO_UNIQUE_VALUE restituisce il valore true per questi tipi di dati.  
  
 Per **varchar**, **nvarchar** e **varbinary**, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client continua a segnalare rispettivamente 8000, 4000 e 8000 per il valore di COLUMN_SIZE, anche se è effettivamente illimitato. Ciò consente di assicurare la compatibilità con le versioni precedenti.  
  
 Per il tipo di dati **XML** , il driver ODBC di Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] segnala SQL_SS_LENGTH_UNLIMITED per COLUMN_SIZE di indicare dimensioni illimitate.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo e parametri con valori di tabella  
 Il tipo di tabella per i parametri con valori di tabella è effettivamente un metatipo, ovvero un tipo usato per definire altri tipi. Non è pertanto necessario che venga esposta tramite SQLGetTypeInfo. Per recuperare i metadati per i tipi di tabella utilizzati con i parametri con valori di tabella, le applicazioni devono utilizzare SQLTables anziché SQLGetTypeInfo.  
  
 Per ulteriori informazioni sul recupero di metadati per i parametri con valori di tabella, vedere [attributi dell'istruzione che influiscono sui parametri con valori di tabella](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere [parametri &#40;con valori di&#41;tabella ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>Supporto di SQLGetTypeInfo per le caratteristiche avanzate di data e ora  
 Per i valori restituiti per i tipi data/ora, vedere [metadati del catalogo](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Per informazioni più generali, vedere [miglioramenti &#40;di data e ora&#41;ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Supporto SQLGetTypeInfo per i tipi CLR definiti dall'utente di grandi dimensioni  
 **SQLGetTypeInfo** supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per ulteriori informazioni, vedere [tipi &#40;CLR definiti dall'utente di grandi&#41;dimensioni ODBC](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
   [funzione SQLGetTypeInfo](https://go.microsoft.com/fwlink/?LinkId=59356)  
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
