---
title: Proprietà (Record ADO) dell'origine | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::Source
- _Record::PutRefSource
- _Record::GetSource
- _Record::put_Source
- _Record::putref_Source
- _Record::get_Source
helpviewer_keywords:
- Source property [ADO Record]
ms.assetid: 2c18279e-6f35-4af0-b12e-8f1543d9ed20
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b1870d8cd8253e1b6de74ce093d51ca6e33c5c6d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930930"
---
# <a name="source-property-ado-record"></a>Proprietà Source (Record - ADO)
Indica l'origine dati o l'oggetto rappresentato dall'elemento di [Record](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **Variant** valore che indica l'entità rappresentata dalle **Record**.  
  
## <a name="remarks"></a>Note  
 Il **origine** proprietà restituisce il *origine* argomento del **Record** oggetto [Open](../../../ado/reference/ado-api/open-method-ado-record.md) (metodo). Può contenere una stringa URL assoluta o relativa. Un URL assoluto può essere usato senza impostazione il [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) per aprire direttamente la **Record** oggetto. Implicita **connessione** viene creato in questo caso l'oggetto.  
  
 Il **origine** proprietà può inoltre contenere un riferimento a un a cui è già aperta **Recordset**, che consente di visualizzare una **Record** oggetto che rappresenta la riga corrente nella  **Recordset**.  
  
 Il **origine** proprietà può contenere anche un riferimento a un [comando](../../../ado/reference/ado-api/command-object-ado.md) object che restituisce una singola riga di dati dal provider.  
  
 Se il **ActiveConnection** anche è impostata, il **origine** proprietà deve puntare a un oggetto esistente all'interno dell'ambito di tale connessione. Ad esempio, nella struttura ad albero degli spazi dei nomi, se il **origine** proprietà contiene un URL assoluto, deve puntare a un nodo esistente all'interno dell'ambito del nodo identificato dall'URL nella stringa di connessione. Se il **origine** proprietà contiene un URL relativo, quindi la convalida avviene all'interno del contesto impostato il **ActiveConnection** proprietà.  
  
 Il **origine** è di lettura/scrittura durante le **Record** oggetto è chiuso ed è di sola lettura mentre il **Record** oggetto è aperto.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà Source (errore ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Proprietà Source (Recordset ADO)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
