---
title: Proprietà (parametro ADO) Size | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3796f772dedb961ec34eb0639034350989f99142
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931059"
---
# <a name="size-property-ado-parameter"></a>Proprietà Size (Parameter - ADO)
Indica la dimensione massima, in byte o caratteri, di un [parametro](../../../ado/reference/ado-api/parameter-object.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **lungo** valore che indica la dimensione massima in byte o caratteri di un valore in un **parametro** oggetto.  
  
## <a name="remarks"></a>Note  
 Usare la **dimensioni** proprietà per determinare le dimensioni massime per i valori scritti o letti nel [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà di un **parametro** oggetto.  
  
 Se si specifica un tipo di dati a lunghezza variabile per una **parametri** oggetto (ad esempio, qualsiasi **stringa** digitare, ad esempio **adVarChar**), è necessario impostare l'oggetto  **Dimensioni** proprietà prima di aggiungerlo per il [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) insieme; in caso contrario, si verifica un errore.  
  
 Se è già stato accodato il **parametro** dell'oggetto per il **parametri** raccolta di un [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto e si modifica il tipo per un tipo di dati a lunghezza variabile, è necessario impostare il **parametro** dell'oggetto **dimensioni** proprietà prima di eseguire il **comando** dell'oggetto; in caso contrario, si verifica un errore.  
  
 Se si usa la [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) metodo per ottenere informazioni sui parametri del provider di e restituisce uno o più tipi di dati a lunghezza variabile **parametro** oggetti, ADO possa allocare memoria per i parametri di base alle relative dimensioni massime possibili, che potrebbe causare un errore durante l'esecuzione. Per evitare un errore, è necessario impostare esplicitamente il **dimensioni** proprietà per tali parametri prima di eseguire il comando.  
  
 Il **dimensioni** è di lettura/scrittura.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione (esempio di proprietà (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni ed esempio di proprietà direzione (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione (esempio di proprietà (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Proprietà Size (flusso ADO)](../../../ado/reference/ado-api/size-property-ado-stream.md)
