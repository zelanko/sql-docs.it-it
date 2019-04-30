---
title: Impostazione di ExtendedAnsiSQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9b8999e229e8a6ed4804b2f06a4072d139ae93a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159361"
---
# <a name="setting-extendedansisql"></a>Impostazione di ExtendedAnsiSQL
L'attributo può essere controllato nella stringa di connessione, aggiungere l'attributo ExtendedAnsiSQL:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (impostazione predefinita)|Questa impostazione non abilita le nuove funzionalità.|  
|ExtendedAnsiSQL=1|Questa impostazione abilita le nuove funzionalità.|  
  
 L'attributo può essere impostato anche in un DSN tramite il **opzioni avanzate** finestra di dialogo quando si configura un DSN tramite Pannello di controllo.  
  
 Impostare l'attributo su 0 disabilita le nuove funzionalità: impostandola su 1 abilita le nuove funzionalità.  
  
 L'attributo può essere impostato anche tramite SQLSetConnectAttr(). Il valore dell'attributo è 65501 e viene impostato su un valore SQLINTEGER pari a 1 o 0, come illustrato nella tabella precedente. Può essere chiamato prima o dopo la connessione, ma è preferibile per chiamarlo dopo la connessione a causa l'ordine in cui i processi del driver memorizzato nella cache gli attributi di connessione e le stringhe di connessione.
