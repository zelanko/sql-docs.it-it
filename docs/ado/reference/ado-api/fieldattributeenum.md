---
title: FieldAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db3b72b7bdaf60febdeb41eb6f6e1e86c5064f63
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653557"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
Specifica uno o più attributi di un [campo](../../../ado/reference/ado-api/field-object.md) oggetto.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|Indica che il provider vengono memorizzati nella cache i valori dei campi e che le letture successive vengono eseguite dalla cache.|  
|**adFldFixed**|0x10|Indica che il campo contiene dati a lunghezza fissa.|  
|**adFldIsChapter**|0x2000|Indica che il campo contiene un valore del capitolo, che specifica un set di record figlio specifici correlati al campo padre. In genere capitolo campi vengono usati con il data shaping o filtri.|  
|**adFldIsCollection**|0x40000|Indica che il campo di specifica che la risorsa rappresentata dal record è una raccolta di altre risorse, ad esempio una cartella, invece di una risorsa semplice, ad esempio un file di testo.|  
|**adFldKeyColumn**|0x8000|Indica che il campo di specifica di tutta o parte di chiave primaria della colonna.|  
|**adFldIsDefaultStream**|0x20000|Indica che il campo contiene il flusso predefinito per la risorsa rappresentata dal record. Ad esempio, il flusso predefinito può essere il contenuto HTML di una cartella radice in un sito Web, che vengono automaticamente resi disponibili quando viene specificato l'URL radice.|  
|**adFldIsNullable**|0x20|Indica che il campo ammette i valori null.|  
|**adFldIsRowURL**|0x10000|Indica che il campo contiene l'URL che denomina la risorsa dall'archivio dati rappresentato dal record.|  
|**adFldLong**|0x80|Indica che il campo è un campo binario long. Indica inoltre che è possibile usare la [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) metodi.|  
|**adFldMayBeNull**|0x40|Indica che è possibile leggere i valori null nel campo.|  
|**adFldMayDefer**|0x2|Indica che il campo è che posticipata è, i valori dei campi non vengono recuperati dall'origine dati con il record completo, ma solo quando si accede in modo esplicito.|  
|**adFldNegativeScale**|0x4000|Indica che il campo rappresenta un valore numerico da una colonna che supporta valori di scala negativo. La scala è specificata per il [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) proprietà.|  
|**adFldRowID**|0x100|Indica che il campo contiene un identificatore di riga persistente che non può essere scritte e non ha alcun valore significativo, ad eccezione per identificare la riga (ad esempio un numero di record, un identificatore univoco e così via).|  
|**adFldRowVersion**|0x200|Indica che il campo contiene un tipo di indicatore di data e ora usato per tenere traccia degli aggiornamenti.|  
|**adFldUnknownUpdatable**|0x8|Indica che il provider non è possibile determinare se è possibile scrivere al campo.|  
|**adFldUnspecified**|-1 0xFFFFFFFF|Indica che il provider non siano specificati gli attributi di campo.|  
|**adFldUpdatable**|0x4|Indica che è possibile scrivere al campo.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.FieldAttribute.CACHEDEFERRED|  
|AdoEnums.FieldAttribute.FIXED|  
|AdoEnums.FieldAttribute.ISNULLABLE|  
|AdoEnums.FieldAttribute.LONG|  
|AdoEnums.FieldAttribute.MAYBENULL|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums.FieldAttribute.ROWID|  
|AdoEnums.FieldAttribute.ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums.FieldAttribute.UNSPECIFIED|  
|AdoEnums.FieldAttribute.UPDATABLE|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Metodo Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Proprietà attributi (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|
