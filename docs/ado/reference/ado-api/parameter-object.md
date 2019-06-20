---
title: Oggetto Parameter | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 152186c0bb1c2fb75197a920e06e0b6bb96dadd0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703313"
---
# <a name="parameter-object"></a>Oggetto Parameter
Rappresenta un parametro o un argomento associato a un [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto basato su una query con parametri o stored procedure.  
  
## <a name="remarks"></a>Note  
 Molti provider supporta i comandi con parametri. Questi sono i comandi in cui l'azione desiderata è definita una sola volta, ma le variabili (o parametri) vengono usati per modificare alcuni dettagli del comando. Ad esempio, un'istruzione SQL SELECT è stato possibile utilizzare un parametro per definire i criteri di corrispondenza di una clausola WHERE e un altro per definire il nome della colonna per una clausola di ordinamento.  
  
 **Parametro** oggetti rappresentano i parametri associati alle query con parametri o gli argomenti in e out e i valori restituiti di stored procedure. A seconda della funzionalità del provider, alcune raccolte, metodi o proprietà di un **parametro** oggetto potrebbe non essere disponibile.  
  
 Con le raccolte, i metodi e proprietà di un **parametro** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Impostare o restituire il nome di un parametro con il [nome](../../../ado/reference/ado-api/name-property-ado.md) proprietà.  
  
-   Ottenere o impostare il valore di un parametro con il [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà. **Valore** è la proprietà predefinita di **parametro** oggetto.  
  
-   Impostare o restituire le caratteristiche del parametro con il [attributi](../../../ado/reference/ado-api/attributes-property-ado.md), [direzione](../../../ado/reference/ado-api/direction-property.md), [precisione](../../../ado/reference/ado-api/precision-property-ado.md), [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md), [ Le dimensioni](../../../ado/reference/ado-api/size-property-ado-parameter.md), e [tipo](../../../ado/reference/ado-api/type-property-ado.md) proprietà.  
  
-   Passare i dati caratteri o binari long a un parametro con il [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) (metodo).  
  
-   Gli attributi specifici del provider di accesso usando il [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
 Se si conoscono i nomi e le proprietà dei parametri associati con la stored procedure o query con parametri che si desidera chiamare, è possibile usare la [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) metodo per creare **parametro** oggetti con le impostazioni di proprietà appropriata e usare la [Append](../../../ado/reference/ado-api/append-method-ado.md) metodo a cui aggiungere i le [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) raccolta. Ciò consente di impostare e restituire i valori dei parametri senza dover chiamare il [aggiornare](../../../ado/reference/ado-api/refresh-method-ado.md) metodo sul **parametri** insieme per recuperare le informazioni sul parametro dal provider, un potenzialmente operazione a elevato utilizzo di risorse.  
  
 Il **parametro** oggetto non sicuro per lo script.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Gli eventi, metodi e proprietà dell'oggetto parametro](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Metodo CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameters Collection (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
