---
title: Messaggi di errore Jet ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec549f256caeab598f6e49632b2a50cfa5841710
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63244611"
---
# <a name="odbc-jet-error-messages"></a>Messaggi di errore Jet ODBC
Per gli errori che si verificano nell'origine dati, il driver ODBC restituisce un messaggio di errore restituito da File di libreria ODBC. Per gli errori che si verificano nel driver ODBC o gestione Driver, driver restituisce un messaggio di errore in base al testo associati con il valore SQLSTATE.  
  
 I messaggi di errore hanno il formato seguente:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 I prefissi tra parentesi quadre ([]) identificano la posizione dell'errore. Quando si verifica l'errore in Gestione Driver *origine dati* non è specificato. Quando si verifica l'errore nell'origine dati, il [*fornitore*] e [*ODBC-componente*] i prefissi di identificano il fornitore e il nome del componente che ha ricevuto l'errore dall'origine dati ODBC.  
  
 Nella tabella seguente mostra i messaggi di errore restituiti dal driver ISAM e gestione Driver:  
  
|Messaggio di errore|Posizione dell'errore|  
|-------------------|--------------------|  
|[Microsoft][ODBC Driver Manager] *message-text*|Gestione driver (Odbc32.dll)|  
|[Microsoft][ODBC *driver-name*]*message-text*|Driver ISAM (vedere Driver ISAM)|
