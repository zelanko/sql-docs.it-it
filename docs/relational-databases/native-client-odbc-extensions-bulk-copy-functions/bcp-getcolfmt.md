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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 40e7f63438bbe6ff68284aa573e1307b17087234
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707540"
---
# <a name="bcp_getcolfmt"></a>bcp_getcolfmt
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
 I valori delle proprietà di formato della colonna sono elencati nell'argomento [bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md) . I valori della proprietà formato colonna vengono impostati chiamando la funzione **bcp_setcolfmt** e la funzione **bcp_getcolfmt** viene utilizzata per trovare il valore della proprietà formato colonna.  
  
 È possibile che vengano osservate le modifiche del comportamento durante la connessione a un computer server [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (o versione successiva) rispetto alle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Metadata Discovery](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="bcp_getcolfmt-support-for-enhanced-date-and-time-features"></a>Supporto di bcp_getcolfmt per le caratteristiche avanzate di data e ora  
 I tipi utilizzati con la proprietà **BCP_FMT_TYPE** per i tipi data/ora sono specificati nelle [modifiche della copia bulk per i tipi &#40;di data e ora avanzati&#41;OLE DB e ODBC](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Per ulteriori informazioni, vedere [miglioramenti &#40;di data e ora&#41;ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
