---
title: Comando SET EXCLUSIVE Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d140c4be3ab850547ac82f9b954e7313b008dbf0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300861"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE (comando)
Specifica se i file di tabella vengono aperti per uso esclusivo o condiviso in una rete.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 Limita l'accessibilità di una tabella aperta in una rete all'utente che l'ha aperta. La tabella non è accessibile ad altri utenti della rete. SET EXCLUSIVE ON impedisce inoltre a tutti gli altri utenti di disporre dell'accesso in sola lettura.  
  
 OFF  
 (Impostazione predefinita per il driver; le impostazioni predefinite per Visual FoxPro sono ON per la sessione dati globale e OFF per una sessione di dati privata.) Consente a una tabella aperta su una rete di essere condivisa e modificata da qualsiasi utente della rete.  
  
## <a name="remarks"></a>Osservazioni  
 La modifica dell'impostazione di SET EXCLUSIVE non modifica lo stato delle tabelle aperte in precedenza. Ad esempio, se una tabella viene aperta con SET EXCLUSIVE impostato su ON e SET EXCLUSIVE viene successivamente modificato in OFF, la tabella mantiene lo stato di utilizzo esclusivo.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo di configurazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
