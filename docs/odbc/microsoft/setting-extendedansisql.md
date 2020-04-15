---
title: Impostazione di ExtendedAnsiSQL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b5c2e4ed4d8bd64d02fb6a62861db832f6b0898
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300801"
---
# <a name="setting-extendedansisql"></a>Impostazione di ExtendedAnsiSQL
L'attributo può essere controllato nella stringa di connessione aggiungendo l'attributo ExtendedAnsiSQL:The attribute can be controlled in the connection string by adding the ExtendedAnsiSQL attribute:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|ExtendedAnsiSQL: 0 (predefinito)|Questa impostazione non abilita le nuove funzionalità.|  
|ExtendedAnsiSQL1|Questa impostazione abilita le nuove funzionalità.|  
  
 L'attributo può essere impostato anche in un DSN tramite la finestra di dialogo **Opzioni avanzate** durante la configurazione di un DSN tramite il Pannello di controllo.  
  
 L'impostazione dell'attributo su 0 disabilita le nuove funzionalità; l'impostazione su 1 abilita le nuove funzioni.  
  
 L'attributo può essere impostato anche utilizzando SQLSetConnectAttr(). Il valore dell'attributo è 65501 e viene impostato su un valore SQLINTEGER pari a 1 o 0, come documentato nella tabella precedente. Può essere chiamato prima o dopo la connessione, ma è preferibile chiamarlo dopo la connessione a causa dell'ordine in cui il driver elabora gli attributi di connessione memorizzati nella cache e le stringhe di connessione.
