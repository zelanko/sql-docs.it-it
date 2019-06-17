---
title: SET DELETED (comando) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5efbd7e98b430128e52634f5c7d71597afc89ace
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127827"
---
# <a name="set-deleted-command"></a>SET DELETED (comando)
Specifica se vengono elaborati i record contrassegnati per l'eliminazione e se sono disponibili per l'uso in altri comandi.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 (Valore predefinito per il driver, il valore predefinito di Visual FoxPro è impostata su OFF). Specifica che i comandi che agiscono su record, compresi i record nelle tabelle correlate, usando un ambito di ignorare i record contrassegnati per l'eliminazione.  
  
 OFF  
 Specifica che i record contrassegnati per l'eliminazione sono accessibili tramite comandi che agiscono sui record, compresi i record nelle tabelle correlate, usando un ambito.  
  
## <a name="remarks"></a>Note  
 Esegue una query che usa DELETED () per testare lo stato di record può essere ottimizzato tramite la tecnologia Visual FoxPro Rushmore se la tabella viene indicizzata in (eliminati).  
  
> [!IMPORTANT]  
>  SET DELETED viene ignorato se l'ambito predefinito per il comando è il record corrente o se si include un ambito di un singolo record. L'indice Ignora SET DELETED sempre e indicizza tutti i record nella tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [DELETE (comando SQL)](../../odbc/microsoft/delete-sql-command.md)
