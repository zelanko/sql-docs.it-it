---
title: Proprietà Sort | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::get_Sort
- Recordset15::put_Sort
- Recordset15::PutSort
- Recordset15::GetSort
- Recordset15::Sort
helpviewer_keywords:
- DESC [ADO]
- ASC [ADO]
- Sort property [ADO]
ms.assetid: 3683ffa0-6f93-4906-9533-ef6942f24f39
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 946314f7be9f6c39d47a3f26b577e10834064dab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930948"
---
# <a name="sort-property"></a>Proprietà Sort
Indica uno o più nomi di campo in cui è ordinato il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) e se ogni campo viene ordinato in ordine crescente o decrescente.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **stringa** che indica i nomi dei campi nel **Recordset** in cui eseguire l'ordinamento. Ogni nome è separato da una virgola e, facoltativamente, è seguito da uno spazio vuoto e dalla parola chiave **ASC**, che ordina il campo in ordine crescente, o **desc**, che ordina il campo in ordine decrescente. Per impostazione predefinita, se non viene specificata alcuna parola chiave, il campo viene ordinato in ordine crescente.  
  
## <a name="remarks"></a>Osservazioni  
 Questa proprietà richiede che la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) sia impostata su **adUseClient**. Viene creato un indice temporaneo per ogni campo specificato nella proprietà **Sort** se non esiste già un indice.  
  
 L'operazione di ordinamento è efficiente perché i dati non vengono ridisposti fisicamente, ma sono semplicemente accessibili nell'ordine specificato dall'indice.  
  
 Quando il valore della proprietà **Sort** è diverso da una stringa vuota, l'ordine delle proprietà di **ordinamento** ha la precedenza sull'ordine specificato in una clausola **Order by** inclusa nell'istruzione SQL usata per aprire il **Recordset**.  
  
 Non è necessario aprire il **Recordset** prima di accedere alla proprietà di **ordinamento** . può essere impostata in qualsiasi momento dopo la creazione di un'istanza dell'oggetto **Recordset** .  
  
 Se si imposta la proprietà **Sort** su una stringa vuota, le righe vengono reimpostate sull'ordine originale ed eliminano gli indici temporanei. Gli indici esistenti non verranno eliminati.  
  
 Si supponga che un **Recordset** contenga tre campi denominati *FirstName*, *middleInitial*e *LastName*. Impostare la proprietà **Sort** sulla stringa "`lastName DESC, firstName ASC`", che ordina il **Recordset** in base al cognome in ordine decrescente, quindi in base al nome in ordine crescente. Il secondo iniziale viene ignorato.  
  
 Nessun campo può essere denominato "ASC" o "DESC" perché questi nomi sono in conflitto con le parole chiave **ASC** e **desc**. È possibile creare un alias per un campo con un nome in conflitto usando la parola chiave **As** nella query che restituisce il **Recordset**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Sort (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Esempio di proprietà Sort (VC + +)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Optimize Property-Dynamic (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Proprietà SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Proprietà SortDirection (Servizi Desktop remoto)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
