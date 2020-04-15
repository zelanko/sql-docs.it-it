---
title: Proprietà SQLParamData . Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a2cc7bfdf35bf30a0883eecf6767e03b6805253
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289061"
---
# <a name="sqlparamdata"></a>SQLParamData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando SQLParamData restituisce *l'oggetto ValuePtrPtr* associato a un parametro con valori di tabella, l'applicazione deve chiamare SQLPutData con *StrLen_Or_Ind*. Se *StrLen_Or_Ind* ha un valore maggiore di 0, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] significa che l'applicazione è pronta per Native Client per raccogliere i dati dei parametri per la riga successiva del parametro con valori di tabella. Se *StrLen_Or_Ind* ha un valore pari a 0, significa che non sono presenti altre righe di dati per il parametro con valori di tabella. Per ulteriori informazioni, vedere [Associazione e trasferimento di dati di parametri con valori di tabella e valori di colonna](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere Parametri con valori di [tabella &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Sqlparamdata](https://go.microsoft.com/fwlink/?LinkId=80706)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
