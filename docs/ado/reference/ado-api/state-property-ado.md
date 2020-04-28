---
title: Proprietà state (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c45b9331ddd538cdf23a57eaf39b6efb71bccc4a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930857"
---
# <a name="state-property-ado"></a>Proprietà State (ADO)
Indica per tutti gli oggetti applicabili se lo stato dell'oggetto è aperto o chiuso. Se l'oggetto esegue un metodo asincrono, indica se lo stato corrente dell'oggetto è la connessione, l'esecuzione o il recupero.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **Long** che può essere un valore [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) . Il valore predefinito è **adStateClosed**.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile utilizzare la proprietà **state** per determinare lo stato corrente di un determinato oggetto in qualsiasi momento.  
  
 La proprietà **state** dell'oggetto può avere una combinazione di valori. Se, ad esempio, un'istruzione è in esecuzione, questa proprietà avrà un valore combinato di **adStateOpen** e **adStateExecuting**.  
  
 La proprietà **state** è di sola lettura.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ConnectionString, ConnectionTimeout e state (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Esempio di proprietà ConnectionString, ConnectionTimeout e state (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
