---
title: Sequenza di fuga delle chiamate di routine Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1194efe6a21c456a722ccd4352661c998f0316d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298221"
---
# <a name="procedure-call-escape-sequence"></a>Sequenza di escape per chiamata di procedura
ODBC utilizza sequenze di escape per le chiamate di routine. La sintassi di questa sequenza di escape è la seguente:The syntax of this escape sequence is as follows:  
  
 **[?]]****chiama** il *nome della routine*[**(**[*parametro*][,[*parametro*]]... **)**]**}**  
  
 Nella notazione BNF, la sintassi è la seguente:  
  
 *ODBC-procedure-escape* ::  
  
 &#124;'inseguitore di chiamata *ODBC-esc-initiator* [? *procedure ODBC-esc-terminator*  
  
 *procedura* :: *nome-procedura* &#124; *nome-procedura* (*procedure-parametro-elenco*)  
  
 *identificatore-procedura* :: : *nome definito dall'utente*  
  
 *nome-procedura* :: : *identificatore-procedura*  
  
 &#124; *nome-proprietario*. *identificatore della procedura*  
  
 &#124; *identificatore-procedura di separazione-catalogo-nome-catalogo* *procedure-identifier*  
  
 &#124; *separatore-catalogo-nome-catalogo* [*nome-proprietario*]. *identificatore della procedura*  
  
 La terza sintassi è valida solo se l'origine dati non supporta i proprietari.  
  
 *proprietario-nome* :: : *nome-definito dall'utente*  
  
 *nome-catalogo* :: *nome-definito dall'utente*  
  
 *separatore di catalogo* *implementation-defined*::  
  
 Il separatore del catalogo viene restituito tramite **SQLGetInfo** con l'opzione di informazioni SQL_CATALOG_NAME_SEPARATOR.  
  
 *procedura-parametro-elenco* :: *: parametro-procedura*  
  
 &#124; *parametro-procedura*, *procedure-parameter-list*  
  
 *procedura-parametro* :: : *parametro dinamico* &#124; *valore letterale* &#124; *stringa vuota*  
  
 *stringa vuota* ::  
  
 *ODBC-esc-initiator* ::  
  
 *Carattere di terminazione ODBC-esc::: *  
  
 Se un parametro di routine è una stringa vuota, la routine utilizza il valore predefinito per tale parametro.  
  
 Per determinare se l'origine dati supporta le procedure e il driver supporta la sintassi di chiamata di procedura ODBC, un'applicazione può chiamare **SQLGetInfo** con il tipo di informazioni SQL_PROCEDURES.
