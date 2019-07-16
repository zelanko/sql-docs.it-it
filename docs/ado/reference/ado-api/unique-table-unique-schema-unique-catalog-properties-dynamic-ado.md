---
title: Controllo modifica alla tabella di Base di Recordset (ADO) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911669"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>Tabella univoca, Schema univoco, univoco del catalogo delle proprietà-dinamica (ADO)
Consente di controllare rigorosamente le modifiche a una tabella di base in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) che è stata formata da un'operazione di JOIN più tabelle di base.  
  
-   **Tabella univoca** specifica il nome della tabella di base su cui sono consentite aggiornamenti, inserimenti ed eliminazioni.  
  
-   **Schema univoco** consente di specificare il *schema*, o il nome del proprietario della tabella.  
  
-   **Catalogo univoca** consente di specificare il *catalogo*, o il nome del database contenente la tabella.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** valore che rappresenta il nome di una tabella, schema o catalogo.  
  
## <a name="remarks"></a>Note  
 La tabella di base desiderata è identificata in modo univoco dal relativo catalogo, schema e i nomi di tabella. Quando la **tabella univoca** è impostata, i valori delle **Schema univoco** o **catalogo univoco** proprietà vengono usate per trovare la tabella di base. È consigliabile, ma non obbligatorio, che una o entrambe le **Schema univoco** e **catalogo univoco** prima di impostare le proprietà il **tabella univoca** è impostata.  
  
 La chiave primaria della **tabelle univoche** viene considerata come chiave primaria dell'intera **Recordset**. Si tratta della chiave che viene usata per qualsiasi metodo che richiede una chiave primaria.  
  
 Anche se **tabelle univoche** è impostata, il [eliminare](../../../ado/reference/ado-api/delete-method-ado-recordset.md) metodo influisce solo sulla tabella denominata. Il [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [Risincronizza](../../../ado/reference/ado-api/resync-method.md), [Update](../../../ado/reference/ado-api/update-method.md), e [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) metodi hanno effetto su qualsiasi tabella di base sottostante del **Recordset**.  
  
 **Tabella univoca** deve essere specificato prima di eseguire qualsiasi risincronizzazione personalizzati. Se **tabelle univoche** non è stato specificato, il [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) proprietà non ha alcun effetto.  
  
 Se non è stata trovata una tabella di base univoca, verrà restituito un errore in fase di esecuzione.  
  
 Queste proprietà dinamiche vengono aggiunti al **Recordset** oggetto [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta quando il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su  **adUseClient**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
