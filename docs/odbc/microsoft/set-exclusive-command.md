---
title: IMPOSTA comando esclusivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d1a37043d332b54d0d5c5ebb7b2ba9f3acce000
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071766"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE (comando)
Specifica se i file di tabella vengono aperti per l'utilizzo esclusivo o condiviso in una rete.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ATTIVA  
 Limita l'accessibilità di una tabella aperta in una rete all'utente che l'ha aperta. La tabella non è accessibile ad altri utenti della rete. SET EXCLUSIVe ON impedisce anche a tutti gli altri utenti di avere accesso in sola lettura.  
  
 OFF  
 (Impostazione predefinita per il driver; le impostazioni predefinite per Visual FoxPro sono attivate per la sessione dati globali e disattivate per una sessione di dati privata). Consente la condivisione e la modifica di una tabella in una rete da parte di qualsiasi utente nella rete.  
  
## <a name="remarks"></a>Osservazioni  
 La modifica dell'impostazione di SET EXCLUSIVe non comporta la modifica dello stato delle tabelle precedentemente aperte. Se, ad esempio, viene aperta una tabella con l'opzione SET EXCLUSIVe impostata su ON e l'opzione SET EXCLUSIVe viene modificata in un secondo momento, la tabella mantiene lo stato di utilizzo esclusivo.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo di configurazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
