---
title: Controllare le modifiche apportate alla tabella di base del recordset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1b70920cd223223d5efb14925a6808168ca9cc16
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67911669"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>Tabella univoca, schema univoco, proprietà del catalogo univoco-Dynamic (ADO)
Consente di controllare in modo accurato le modifiche apportate a una determinata tabella di base in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) costituito da un'operazione di join in più tabelle di base.  
  
-   **Tabella univoca** specifica il nome della tabella di base su cui sono consentiti aggiornamenti, inserimenti ed eliminazioni.  
  
-   **Schema univoco** specifica lo *schema*o il nome del proprietario della tabella.  
  
-   **Unique Catalog** specifica il *Catalogo*o il nome del database che contiene la tabella.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **stringa** che rappresenta il nome di una tabella, di uno schema o di un catalogo.  
  
## <a name="remarks"></a>Osservazioni  
 La tabella di base desiderata viene identificata in modo univoco dai relativi nomi di catalogo, schema e tabella. Quando viene impostata la proprietà di **tabella univoca** , per trovare la tabella di base vengono utilizzati i valori delle proprietà univoche **dello schema** o del **catalogo univoco** . È previsto, ma non obbligatorio, che sia l'impostazione **dello schema univoco** che delle proprietà del **Catalogo univoche** prima che venga impostata la proprietà della **tabella univoca** .  
  
 La chiave primaria della **tabella univoca** viene considerata come la chiave primaria dell'intero **Recordset**. Si tratta della chiave utilizzata per qualsiasi metodo che richiede una chiave primaria.  
  
 Mentre la **tabella Unique** è impostata, il metodo [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md) influisca solo sulla tabella denominata. I metodi [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [Update](../../../ado/reference/ado-api/update-method.md)e [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) influiscono su tutte le tabelle di base sottostanti appropriate del **Recordset**.  
  
 Prima di eseguire qualsiasi operazione di risincronizzazione personalizzata, è necessario specificare una **tabella univoca** . Se non è stata specificata una **tabella univoca** , la proprietà del [comando di risincronizzazione](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) non avrà alcun effetto.  
  
 Se non è possibile trovare una tabella di base univoca, viene restituito un errore di run-time.  
  
 Queste proprietà dinamiche vengono tutte aggiunte alla raccolta delle [Proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) dell'oggetto **Recordset** quando la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
