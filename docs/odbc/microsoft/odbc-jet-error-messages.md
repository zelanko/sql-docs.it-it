---
title: Messaggi di errore di ODBC Jet | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81293111"
---
# <a name="odbc-jet-error-messages"></a>Messaggi di errore Jet ODBC
Per gli errori che si verificano nell'origine dati, il driver ODBC restituisce un messaggio di errore restituito dalla libreria di file ODBC. Per gli errori che si verificano nel driver ODBC o in Gestione driver, il driver restituisce un messaggio di errore in base al testo associato a SQLSTATE.  
  
 Il formato dei messaggi di errore è il seguente:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 I prefissi tra parentesi quadre ([]) identificano la posizione dell'errore. Quando l'errore si verifica in Gestione driver, l' *origine dati* non viene specificata. Quando l'errore si verifica nell'origine dati, i prefissi [*Vendor*] e [*ODBC-Component*] identificano il fornitore e il nome del componente ODBC che ha ricevuto l'errore dall'origine dati.  
  
 Nella tabella seguente vengono illustrati i messaggi di errore restituiti da Gestione driver e da ISAM driver:  
  
|Messaggio di errore|Percorso errore|  
|-------------------|--------------------|  
|Microsoft [Gestione driver ODBC] *testo del messaggio*|Gestione driver (odbc32. dll)|  
|Microsoft [ *Nome-driver*ODBC] *testo del messaggio*|ISAM del driver (vedere ISAM del driver)|
