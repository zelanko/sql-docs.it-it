---
title: Modifiche al comportamento di sottostringa e lunghezza stringa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4d793720638ee4a98d99e6a915457d8657a1c325
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369083"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>Modifiche al comportamento di sottostringa e lunghezza stringa
  Il [funzione string-length &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length) e [substring-funzione &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring) funzioni possono restituire risultati diversi se utilizzate con database XML che contengono caratteri surrogati.  
  
## <a name="description"></a>Descrizione  
 Quando un database è impostato per essere compatibile con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], il comportamento del [funzione string-length &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length) e [substring-funzione &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring) modifiche di funzioni quando si utilizzano caratteri supplementari Unicode. Ogni carattere supplementare Unicode, definito mediante un punto di codice maggiore di U+FFFF, viene contato come un carattere anziché due da queste funzioni, come nelle versioni precedenti.  
  
 Per altre informazioni sui caratteri surrogati, vedere [caratteri surrogati e supplementari](https://go.microsoft.com/fwlink/?LinkId=178317).  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
