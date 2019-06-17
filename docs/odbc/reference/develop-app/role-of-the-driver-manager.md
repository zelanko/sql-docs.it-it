---
title: Ruolo di gestione Driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 485cd951992ed427461e497c53d17a4f6db24a38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127249"
---
# <a name="role-of-the-driver-manager"></a>Ruolo di Gestione driver
Gestione Driver determina l'ordine finale in cui restituire i record di stato che genera. In particolare, determina quali record ha il valore più alto e deve essere restituito prima di tutto. Il driver è responsabile per l'ordinamento dei record di stato che genera. Se i record di stato vengono inviati da Gestione Driver e il driver, Driver Manager è responsabile ordinandoli. Per altre informazioni, vedere [sequenza di record di stato](../../../odbc/reference/develop-app/sequence-of-status-records.md).  
  
 Il gestore di Driver non quante controllo degli errori possibile. In questo modo ogni driver di controllo per gli stessi errori. Ad esempio, se un argomento di funzione accetta un numero discreto di valori, ad esempio *operazione* nelle **SQLSetPos**, gestione Driver controlla che il valore specificato è valido.  
  
 Le sezioni seguenti descrivono i tipi di condizioni controllate da Gestione Driver. Non sono progettati per essere ritenute esaustive; per un elenco completo del SQLSTATEs restituisce gestione Driver, vedere la sezione "Diagnostica" di ogni funzione. la descrizione di ogni controllo apportata da Gestione Driver viene avviato con le lettere "(DM)". Vedere anche le tabelle di transizione di stato in [appendice b: Tabelle della transizione di stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); da Gestione Driver vengono rilevati errori indicati tra parentesi.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Controlli del valore dell'argomento](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Controlli della transizione di stato](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Controlli degli errori generali](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Errore di Gestione driver e controlli di avviso](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
