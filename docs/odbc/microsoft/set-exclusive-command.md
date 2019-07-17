---
title: SET Exclusive (comando) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071766"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE (comando)
Specifica se i file di tabella vengono aperti per l'uso esclusivo o condiviso in una rete.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 Limita accesso facilitato di una tabella aperta in una rete per l'utente che è stato aperto. La tabella non è accessibile ad altri utenti nella rete. SET esclusivo ON impedisce inoltre tutti gli altri utenti con accesso in sola lettura.  
  
 OFF  
 (Valore predefinito per il driver; i valori predefiniti per Visual FoxPro ON per la sessione di dati globali e OFF per una sessione di dati privati.) Consente a una tabella aperta in una rete per essere condivisi e modificato da alcun utente nella rete.  
  
## <a name="remarks"></a>Note  
 Modifica dell'impostazione di SET esclusivo non cambia lo stato delle tabelle aperte in precedenza. Ad esempio, se una tabella viene aperto con SET esclusivo impostata su ON e SET esclusivo viene modificato in seguito su OFF, la tabella mantiene lo stato di utilizzo esclusivo.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo di configurazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
