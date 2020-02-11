---
title: bcp_getcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_getcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_getcolfmt function
ms.assetid: f8bdada5-7b2d-4475-8c98-f93e9d77b130
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db8b433652829b16890552a70bd1e0d08d1c1bc4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62689082"
---
# <a name="bcp_getcolfmt"></a>bcp_getcolfmt
  Utilizzato per trovare il valore della proprietà di formato di colonna.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_getcolfmt (  
HDBC   
hdbc  
,  
INT   
field  
,  
INT   
property  
,  
void*   
pValue  
,  
INT   
cbvalue,  
INT*   
pcbLen  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
 *campo*  
 Numero di colonna per cui viene recuperata la proprietà.  
  
 *Proprietà*  
 Una delle costanti di proprietà.  
  
 *pValue*  
 Puntatore al buffer dal quale recuperare il valore della proprietà.  
  
 *cbValue*  
 Lunghezza in byte del buffer delle proprietà.  
  
 *pcbLen*  
 IIndicatore di misura relativo alla lunghezza dei dati restituiti nel buffer delle proprietà.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Osservazioni  
 I valori delle proprietà di formato della colonna sono elencati nell'argomento [bcp_setcolfmt](bcp-setcolfmt.md) . I valori delle proprietà di formato della colonna vengono impostati chiamando la funzione **bcp_setcolfmt** e viene utilizzata la funzione **bcp_getcolfmt** per individuare il valore della proprietà formato colonna.  
  
 Le modifiche del comportamento possono essere osservate quando [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ci si connette a un computer server (o versione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] successiva) rispetto alle versioni precedenti. Per altre informazioni, vedere [Metadata Discovery](../native-client/features/metadata-discovery.md).  
  
## <a name="bcp_getcolfmt-support-for-enhanced-date-and-time-features"></a>Supporto di bcp_getcolfmt per le caratteristiche avanzate di data e ora  
 I tipi utilizzati con la `BCP_FMT_TYPE` proprietà per i tipi data/ora sono specificati nelle [modifiche della copia bulk per i tipi di data e ora avanzati &#40;OLE DB e&#41;ODBC ](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Per ulteriori informazioni, vedere [miglioramenti di data e ora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
