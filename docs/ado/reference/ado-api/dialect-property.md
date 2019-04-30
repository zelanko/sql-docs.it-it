---
title: Proprietà Dialect | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::Dialect
helpviewer_keywords:
- Dialect property
ms.assetid: 329c3a71-ba88-4009-b04f-2f52195a5957
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef18eb3d6251bc07ae25ef8cbc3445a87b8390b4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63180287"
---
# <a name="dialect-property"></a>Proprietà Dialect
Indica il dialetto del [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) oppure [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) proprietà. Il sottolinguaggio definisce la sintassi e le regole generali utilizzata dal provider di analisi di flusso o nella stringa.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Il **sottolinguaggio** proprietà contiene un GUID valido che rappresenta il sottolinguaggio di un flusso o il testo del comando. Il valore predefinito per questa proprietà è {C8B521FB-5CF3-11CE-ADE5-00AA0044773D}, che indica che il provider deve scegliere come interpretare il testo del comando o un flusso.  
  
## <a name="remarks"></a>Note  
 ADO non esegue una query del provider quando l'utente legge il valore di questa proprietà. Restituisce una rappresentazione di stringa del valore attualmente archiviato nel [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto.  
  
 Quando l'utente imposta il **sottolinguaggio** proprietà, ADO convalida il GUID e genera un errore se il valore fornito non è un GUID valido. Vedere la documentazione relativa al provider per determinare i valori GUID supportati dal **sottolinguaggio** proprietà.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)
