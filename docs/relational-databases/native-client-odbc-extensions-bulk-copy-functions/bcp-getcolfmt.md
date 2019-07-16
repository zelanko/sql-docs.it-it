---
title: bcp_getcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_getcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7aec6cf3345a0693384835f433bd445fd5079c82
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895677"
---
# <a name="bcpgetcolfmt"></a>bcp_getcolfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Utilizzato per trovare il valore della proprietà di formato di colonna.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_getcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbvalue,  
        INT* pcbLen);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
 *field*  
 Numero di colonna per cui viene recuperata la proprietà.  
  
 *property*  
 Una delle costanti di proprietà.  
  
 *pValue*  
 Puntatore al buffer dal quale recuperare il valore della proprietà.  
  
 *cbValue*  
 Lunghezza in byte del buffer delle proprietà.  
  
 *pcbLen*  
 IIndicatore di misura relativo alla lunghezza dei dati restituiti nel buffer delle proprietà.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Note  
 Valori di proprietà di formato di colonna sono elencati nel [bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md) argomento. I valori di proprietà formato di colonna vengono impostati chiamando il **bcp_setcolfmt** funzione e il **bcp_getcolfmt** funzione viene utilizzata per trovare il valore di proprietà di formato di colonna.  
  
 Modifiche del comportamento possono essere ottenute durante la connessione a un [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (o versione successiva) computer del server, rispetto alle versioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versioni. Per altre informazioni, vedere [Metadata Discovery](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="bcpgetcolfmt-support-for-enhanced-date-and-time-features"></a>Supporto di bcp_getcolfmt per le caratteristiche avanzate di data e ora  
 I tipi utilizzati con il **BCP_FMT_TYPE** sono di proprietà per i tipi di data/ora come specificato nella [modifiche apportate alla copia Bulk per avanzate di data e ora tipi &#40;OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Per altre informazioni, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
