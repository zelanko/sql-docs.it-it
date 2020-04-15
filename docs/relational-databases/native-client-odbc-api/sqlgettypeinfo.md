---
title: Proprietà SQLGetTypeInfo . Documenti Microsoft
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 81ba57c6e66f156f13055ff5ec941fa8f0c86381
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298443"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client segnala la colonna aggiuntiva USERTYPE nel set di risultati di **SQLGetTypeInfo**. USERTYPE riporta la definizione del tipo di dati DB-Library e risulta utile agli sviluppatori che trasferiscono applicazioni DB-Library esistenti a ODBC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tratta l'identità come attributo, mentre ODBC la tratta come tipo di dati. Per risolvere questa mancata corrispondenza, **SQLGetTypeInfo** restituisce i tipi di dati: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity**e **numericidentity**. Il **SQLGetTypeInfo** colonna del set di risultati AUTO_UNIQUE_VALUE indica il valore TRUE per questi tipi di dati.  
  
 Per **varchar**, **nvarchar** e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varbinary**, il driver ODBC Native Client continua a segnalare rispettivamente 8000, 4000 e 8000 per il valore COLUMN_SIZE, anche se in realtà è illimitato. Ciò consente di assicurare la compatibilità con le versioni precedenti.  
  
 Per il tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati **xml,** il driver ODBC Native Client segnala SQL_SS_LENGTH_UNLIMITED per COLUMN_SIZE indicare dimensioni illimitate.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo e parametri con valori di tabella  
 Il tipo di tabella per i parametri con valori di tabella è in effetti un meta-tipo, ovvero un tipo utilizzato per definire altri tipi. Pertanto, non deve essere esposto tramite SQLGetTypeInfo.Therefore, it does not have to be exposed through SQLGetTypeInfo. Le applicazioni devono utilizzare SQLTables, anziché SQLGetTypeInfo, per recuperare i metadati per i tipi di tabella utilizzati con i parametri con valori di tabella.  
  
 Per ulteriori informazioni sul recupero di metdata per i parametri con valori di tabella, vedere [Attributi di istruzione che influiscono sui parametri con valori](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)di tabella .  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere Parametri con valori di [tabella &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>Supporto di SQLGetTypeInfo per le caratteristiche avanzate di data e ora  
 Per i valori restituiti per i tipi di data/ora, vedere [Metadati del catalogo](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Per ulteriori informazioni generali, vedere Miglioramenti di [data e ora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Supporto SQLGetTypeInfo per i tipi CLR definiti dall'utente di grandi dimensioni  
 **SQLGetTypeInfo** supporta tipi CLR definiti dall'utente (UDT) di grandi dimensioni. Per ulteriori informazioni, vedere [Tipi CLR di grandi dimensioni definiti dall'utente &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLGetTypeInfoSQLGetTypeInfo Function](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
