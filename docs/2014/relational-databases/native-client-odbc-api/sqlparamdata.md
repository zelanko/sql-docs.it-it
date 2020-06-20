---
title: SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
author: rothja
ms.author: jroth
ms.openlocfilehash: a4e0e8b31a65f28ce83e0d114231bdedd7a35a4c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021969"
---
# <a name="sqlparamdata"></a>SQLParamData
  Quando SQLParamData restituisce il *ValuePtrPtr* associato a un parametro con valori di tabella, l'applicazione deve chiamare SQLPutData con *StrLen_Or_Ind*. Se *StrLen_Or_Ind* ha un valore maggiore di 0, significa che l'applicazione è pronta per la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] raccolta di dati di parametro da parte di Native Client per la successiva riga di parametri con valori di tabella. Se *StrLen_Or_Ind* ha un valore pari a 0, significa che non sono presenti più righe di dati per il parametro con valori di tabella. Per ulteriori informazioni, vedere [associazione e trasferimento dati di parametri con valori di tabella e valori di colonna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLParamData](/sql/odbc/reference/syntax/sqlparamdata-function)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
