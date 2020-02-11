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
ms.openlocfilehash: 330b55ef2d4fee090c453990d3fe75e6e2dacb6f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063603"
---
# <a name="setting-extendedansisql"></a>Impostazione di ExtendedAnsiSQL
L'attributo può essere controllato nella stringa di connessione aggiungendo l'attributo ExtendedAnsiSQL:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (impostazione predefinita)|Questa impostazione non Abilita le nuove funzionalità.|  
|ExtendedAnsiSQL = 1|Questa impostazione Abilita le nuove funzionalità.|  
  
 L'attributo può essere impostato anche in un DSN tramite la finestra di dialogo **Opzioni avanzate** quando si configura un DSN tramite il pannello di controllo.  
  
 Se si imposta l'attributo su 0, verranno disabilitate le nuove funzionalità. l'impostazione di su 1 Abilita le nuove funzionalità.  
  
 L'attributo può essere impostato anche tramite SQLSetConnectAttr (). Il valore dell'attributo è 65501 e è impostato su un valore SQLINTEGER pari a 1 o 0, come descritto nella tabella precedente. Può essere chiamata prima o dopo la connessione, ma è preferibile chiamarla dopo la connessione a causa dell'ordine in cui il driver elabora gli attributi di connessione memorizzati nella cache e le stringhe di connessione.
