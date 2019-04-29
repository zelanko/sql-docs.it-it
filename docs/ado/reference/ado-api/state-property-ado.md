---
title: Stato proprietà (ADO) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 98d3e61b37eb22ebaf793252f49b2b11621abd80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027666"
---
# <a name="state-property-ado"></a>Proprietà State (ADO)
Indica tutti gli oggetti applicabili se lo stato dell'oggetto è aperto o chiuso. Se l'oggetto è in esecuzione un metodo asincrono, indica se lo stato corrente dell'oggetto è la connessione, l'esecuzione o il recupero.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **lungo** valore che può essere un' [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) valore. Il valore predefinito è **adStateClosed**.  
  
## <a name="remarks"></a>Note  
 È possibile usare la **stato** proprietà per determinare lo stato corrente di un determinato oggetto in qualsiasi momento.  
  
 L'oggetto **stato** proprietà può avere una combinazione di valori. Ad esempio, se un'istruzione è in esecuzione, questa proprietà sarà necessario un valore combinato del **adStateOpen** e **adStateExecuting**.  
  
 Il **stato** proprietà è di sola lettura.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [ConnectionString, ConnectionTimeout ed esempio di proprietà State (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Esempio ConnectionString, ConnectionTimeout e proprietà State (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
