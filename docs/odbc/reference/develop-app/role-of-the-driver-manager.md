---
description: Ruolo di Gestione driver
title: Ruolo di gestione driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f974fe6436173b55f39aced45cc38312221cffaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465658"
---
# <a name="role-of-the-driver-manager"></a>Ruolo di Gestione driver
Gestione driver determina l'ordine finale in cui restituire i record di stato generati. In particolare, determina quale record ha il rango più alto e deve essere restituito per primo. Il driver è responsabile dell'ordinamento dei record di stato generati. Se i record di stato vengono pubblicati da Gestione driver e dal driver, gestione driver è responsabile dell'ordinamento. Per ulteriori informazioni, vedere [sequenza di record di stato](../../../odbc/reference/develop-app/sequence-of-status-records.md).  
  
 Gestione driver esegue il controllo degli errori nel modo più possibile. In questo modo, ogni driver controlla gli stessi errori. Se, ad esempio, un argomento della funzione accetta un numero discreto di valori, ad esempio l' *operazione* in **SQLSetPos**, gestione driver verifica che il valore specificato sia valido.  
  
 Nelle sezioni seguenti vengono descritti i tipi di condizioni controllati da Gestione driver. Non sono destinati a essere completi; per un elenco completo dei SQLState restituiti da Gestione driver, vedere la sezione "diagnostica" di ogni funzione. la descrizione di ogni controllo eseguito da Gestione driver inizia con le lettere "(DM)". Vedere anche le tabelle di transizione dello stato in [Appendice B: tabelle di transizione dello stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); gli errori visualizzati tra parentesi vengono rilevati da Gestione driver.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Controlli del valore dell'argomento](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Controlli della transizione di stato](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Controlli degli errori generali](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Errore di Gestione driver e controlli di avviso](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
