---
title: Proprietà DefaultDatabase | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2eb89353c29ae58194f89b48502f0a9cc5522b58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695449"
---
# <a name="defaultdatabase-property"></a>Proprietà DefaultDatabase
Indica il database predefinito per un [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** valore che restituisce il nome di un database disponibile dal provider.  
  
## <a name="remarks"></a>Note  
 Usare la **DefaultDatabase** proprietà per impostare o restituire il nome del database predefinito per uno specifico **connessione** oggetto.  
  
 Se è presente un database predefinito, le stringhe SQL possono usare una sintassi non qualificata per accedere agli oggetti in tale database. Per accedere agli oggetti in un database diverso da quello specificato nella **DefaultDatabase** proprietà, è necessario qualificare i nomi degli oggetti con il nome del database desiderato. Al momento della connessione, il provider scriverà le informazioni di database predefinito per il **DefaultDatabase** proprietà. Alcuni provider consentono un solo database per ogni connessione, nel qual caso non è possibile modificare il **DefaultDatabase** proprietà.  
  
 Alcune origini dati e provider potrebbero non supportare questa funzionalità e può restituire un errore o una stringa vuota.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** questa proprietà non è disponibile in un client-side **connessione** oggetto.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà DefaultDatabase (VB) e provider](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Esempio di proprietà Provider e DefaultDatabase (VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   
