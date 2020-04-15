---
title: Ruolo di Gestione Driver Documenti Microsoft
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
ms.openlocfilehash: ee3d704ea43125c3cd912a4e67d90bf5d50c733e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304302"
---
# <a name="role-of-the-driver-manager"></a>Ruolo di Gestione driver
Gestione Driver determina l'ordine finale in cui restituire i record di stato che genera. In particolare, determina quale record ha il rango più alto e deve essere restituito per primo. Il driver è responsabile dell'ordinamento dei record di stato generati. Se i record di stato vengono registrati sia da Gestione Driver che dal driver, Gestione Driver è responsabile dell'ordinazione. Per ulteriori informazioni, consultate [Sequenza dei record di stato.](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
 Gestione Driver esegue il maggior numero possibile di controllo degli errori. In questo modo ogni driver non verifica la presenza degli stessi errori. Ad esempio, se un argomento di funzione accetta un numero discreto di valori, ad esempio *Operation* in **SQLSetPos**, Gestione Driver verifica che il valore specificato sia valido.  
  
 Nelle sezioni seguenti vengono descritti i tipi di condizioni controllati da Gestione Driver. Non sono destinati ad essere esaustivi; per un elenco completo di SQLSTATEs restituito da Gestione Driver, vedere la sezione "Diagnostica" di ogni funzione; la descrizione di ogni controllo effettuato da Gestione Driver inizia con le lettere "(DM)". Vedere anche le tabelle di transizione dello stato [nell'Appendice B: Tabelle](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)di transizione dello stato ODBC ; gli errori visualizzati tra parentesi vengono rilevati da Gestione Driver.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Controlli del valore dell'argomento](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Controlli della transizione di stato](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Controlli degli errori generali](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Errore di Gestione driver e controlli di avviso](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
