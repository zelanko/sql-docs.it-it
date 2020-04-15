---
title: Messaggi di errore Jet ODBC - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8fa6e672b69c7791e66dc3919e6fcd22b7c3de7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293111"
---
# <a name="odbc-jet-error-messages"></a>Messaggi di errore Jet ODBC
Per gli errori che si verificano nell'origine dati, il driver ODBC restituisce un messaggio di errore restituito dalla libreria di file ODBC. Per gli errori che si verificano nel driver ODBC o gestione Driver, il driver restituisce un messaggio di errore basato sul testo associato a SQLSTATE.  
  
 I messaggi di errore hanno il seguente formato:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 I prefissi tra parentesi quadre ([ ]) identificano la posizione dell'errore. Quando si verifica l'errore in Gestione Driver, *l'origine dati* non viene fornita. Quando si verifica l'errore nell'origine dati, i prefissi [*vendor*] e [*ODBC-component*] identificano il fornitore e il nome del componente ODBC che ha ricevuto l'errore dall'origine dati.  
  
 Nella tabella seguente vengono illustrati i messaggi di errore restituiti da Gestione Driver e dal driver ISAM:  
  
|Messaggio di errore|Posizione dell'errore|  
|-------------------|--------------------|  
|[Microsoft] [Gestione driver ODBC] *testo del messaggio*|Gestione Driver (Odbc32.dll)|  
|[Microsoft] [Nome *driver*ODBC ] *testo del messaggio*|ISAM del driver (vedere ISAM driver)|
