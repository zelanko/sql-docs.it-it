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
manager: jroth
ms.openlocfilehash: 092eb49216874a59e4bcba09431fcc01dc3679a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711154"
---
# <a name="sort-property"></a>Proprietà Sort
Indica uno o più nomi di campo in cui il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) è ordinato, e se ogni campo è ordinata in ordine crescente o decrescente.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** i nomi di valore che indica il campo nel **Recordset** sul quale eseguire l'ordinamento. Ogni nome è separato da una virgola e viene seguito facoltativamente da uno spazio vuoto e la parola chiave **ASC**, che prevede l'ordinamento in ordine crescente, il campo o **DESC**, che consente di ordinare il campo in ordine decrescente. Per impostazione predefinita, se non viene specificata alcuna parola chiave, il campo viene ordinato in ordine crescente.  
  
## <a name="remarks"></a>Note  
 Questa proprietà richiede la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà viene impostata su **adUseClient**. Verrà creato un indice temporaneo per ogni campo specificato nel **ordinamento** proprietà se non ne esiste già.  
  
 L'operazione di ordinamento è efficiente poiché i dati non vengono riorganizzati fisicamente, ma sono semplicemente possibile accedere nell'ordine specificato dall'indice.  
  
 Quando il valore del **ordinamento** proprietà è diversa da una stringa vuota, il **ordinamento** ordine della proprietà ha la precedenza sull'ordine specificato un **ORDER BY** clausola incluse nell'istruzione SQL utilizzata per aprire la **Recordset**.  
  
 Il **Recordset** non devono essere aperte prima di accedere al **Sort** proprietà; può essere impostata in qualsiasi momento dopo la **Recordset** viene creata un'istanza di oggetto.  
  
 Impostando il **ordinamento** proprietà in una stringa vuota verrà ripristinato l'ordine originale delle righe ed eliminare indici temporanei. Gli indici esistenti non verranno eliminati.  
  
 Si supponga che un **Recordset** contiene tre campi denominati *firstName*, *middleInitial*, e *lastName*. Impostare il **ordinamento** proprietà nella stringa, "`lastName DESC, firstName ASC`", che ordinerà i **Recordset** in base al cognome in ordine decrescente e quindi in base al nome in ordine crescente. Il secondo nome viene ignorato.  
  
 Nessun campo può essere denominato "ASC" o "DESC" in quanto tali nomi siano in conflitto con le parole chiave **ASC** e **DESC**. È possibile creare un alias per un campo con un nome in conflitto con il **AS** parola chiave nella query che restituisce il **Recordset**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Sort (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Esempio di proprietà Sort (VC + +)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Ottimizzare la proprietà dinamica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Proprietà SortColumn (Servizi Desktop remoto)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Proprietà SortDirection (Servizi Desktop remoto)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
