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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e6d813848a45326ee9a74ea38616ceef9dd02cd5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63015683"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la colonna aggiuntiva USERTYPE nel risultato del set di report di driver ODBC Native Client **SQLGetTypeInfo**. USERTYPE riporta la definizione del tipo di dati DB-Library e risulta utile agli sviluppatori che trasferiscono applicazioni DB-Library esistenti a ODBC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tratta l'identità come attributo, mentre ODBC la tratta come tipo di dati. Per risolvere questa mancata corrispondenza, **SQLGetTypeInfo** restituisce i tipi di dati: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity**, e **numericidentity**. Il **SQLGetTypeInfo** colonna AUTO_UNIQUE_VALUE del set di risultati indica il valore TRUE per questi tipi di dati.  
  
 Per la **varchar**, **nvarchar** e **varbinary**, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client continua a segnalare 8000, 4000 e 8000 rispettivamente per il valore di COLUMN_SIZE il valore, anche se non esiste effettivamente alcun limite. Ciò consente di assicurare la compatibilità con le versioni precedenti.  
  
 Per il **xml** tipo di dati, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client riporta SQL_SS_LENGTH_UNLIMITED per COLUMN_SIZE indicare dimensioni illimitate.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo e parametri con valori di tabella  
 Il tipo di tabella per i parametri con valori di tabella è effettivamente un meta-tipo-che è, un tipo usato per definire altri tipi. Pertanto, è privo di essere esposti mediante SQLGetTypeInfo. Le applicazioni devono usare SQLTables, anziché SQLGetTypeInfo, per recuperare i metadati per i tipi di tabella utilizzati con i parametri con valori di tabella.  
  
 Per altre informazioni sul recupero di metadati per parametri con valori di tabella, vedere [gli attributi delle istruzioni che per i parametri Affect Table-Valued](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Per altre informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>Supporto di SQLGetTypeInfo per le caratteristiche avanzate di data e ora  
 Per i valori restituiti per i tipi data/ora, vedere [metadati del catalogo](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Per altre informazioni generali, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Supporto SQLGetTypeInfo per i tipi CLR definiti dall'utente di grandi dimensioni  
 **SQLGetTypeInfo** supporta grandi CLR tipi definiti dall'utente (UDT). Per altre informazioni, vedere [Large CLR User-Defined tipi &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLGetTypeInfo](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
