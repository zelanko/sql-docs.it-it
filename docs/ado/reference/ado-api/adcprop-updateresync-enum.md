---
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6ae4a8adbadc97ad2ea5e3659187481fa71e81b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698868"
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
Specifica se il [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) metodo è seguito da implicita [Risincronizza](../../../ado/reference/ado-api/resync-method.md) operazione del metodo e in questo caso, l'ambito di tale operazione.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|Richiama **Risincronizza** con il valore combinato di tutti gli altri membri ADCPROP_UPDATERESYNC_ENUM.|  
|**adResyncAutoIncrement**|1|Valore predefinito. Tenta di recuperare il nuovo valore identity per le colonne automaticamente incrementato o generati dall'origine dati, ad esempio campi Microsoft Jet contatore o colonne di identità di Microsoft SQL Server.|  
|**adResyncConflicts**|2|Richiama **Risincronizza** per tutte le righe in cui l'operazione update o delete non è riuscita a causa di un conflitto di concorrenza.|  
|**adResyncInserts**|8|Richiama **Risincronizza** per tutte le righe inserite correttamente. Tuttavia, i valori delle colonne AutoIncrement non vengano sincronizzati. Al contrario, il contenuto di nuove righe inserite viene risincronizzato in base al valore di chiave primaria esistente. Se la chiave primaria è un valore di incremento automatico **Risincronizza** non recuperare il contenuto della riga desiderata. Per i valori di chiave primaria a incremento automatico a incremento automatico, chiamare **UpdateBatch** con il valore combinato **adResyncAutoIncrement** + **adResyncInserts**.|  
|**adResyncNone**|0|Non richiama **Risincronizza**.|  
|**adResyncUpdates**|4|Richiama **Risincronizza** per tutte le righe sono state aggiornate.|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà dinamica Update Resync (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
