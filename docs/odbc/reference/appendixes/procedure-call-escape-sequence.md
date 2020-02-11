---
title: Sequenza di escape della chiamata di procedura | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa936eb9f8ef3328945d4ece63fb36432a5fd618
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100595"
---
# <a name="procedure-call-escape-sequence"></a>Sequenza di escape per chiamata di procedura
ODBC utilizza sequenze di escape per le chiamate di routine. La sintassi di questa sequenza di escape è la seguente:  
  
 **{**[? =]**Call** *-routine-nome*[**(**[*parametro*] [, [*parametro*]]... **)**]**}**  
  
 Nella notazione BNF la sintassi è la seguente:  
  
 *ODBC-procedura-Escape* :: =  
  
 &#124; *ODBC-ESC-initiator* [? =] *procedura di chiamata ODBC-ESC-Terminator*  
  
 *procedura* :: = *nome-* procedura &#124; *Procedura-nome* (routine-*parameter-list*)  
  
 *procedure-Identifier* :: = *nome-definito dall'utente*  
  
 *routine-Name* :: = *ID procedura*  
  
 &#124; *nome-proprietario*. *identificatore di routine*  
  
 &#124; catalogo *-nome catalogo-procedura separatore* *-identificatore*  
  
 &#124; nome-catalogo- *separatore* [nome-*proprietario*]. *identificatore di routine*  
  
 La terza sintassi è valida solo se l'origine dati non supporta i proprietari.  
  
 nome- *proprietario* :: = *nome-definito dall'utente*  
  
 nome- *Catalogo* :: = *nome-definito dall'utente*  
  
 *separatore di catalogo* :: = {*definito dall'implementazione*}  
  
 Il separatore di catalogo viene restituito tramite **SQLGetInfo** con l'opzione SQL_CATALOG_NAME_SEPARATOR Information.  
  
 *routine-parameter-list* :: = *parametro di routine*  
  
 Routine di &#124; *parametro*, *procedure-parameter-list*  
  
 *routine-Parameter* :: = *parametro dinamico* &#124; *valore letterale* &#124; *stringa vuota*  
  
 *stringa vuota* :: =  
  
 *ODBC-ESC-initiator* :: = {  
  
 *ODBC-ESC-Terminator* :: =}  
  
 Se un parametro di routine è una stringa vuota, la procedura utilizzerà il valore predefinito per il parametro.  
  
 Per determinare se l'origine dati supporta le procedure e se il driver supporta la sintassi di chiamata della procedura ODBC, un'applicazione può chiamare **SQLGetInfo** con il tipo di informazioni SQL_PROCEDURES.
