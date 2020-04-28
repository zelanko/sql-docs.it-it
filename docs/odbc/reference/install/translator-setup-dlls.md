---
title: Dll di installazione di Translator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28c354fddb36b9e035361fa4ba03fbde34b7d399
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296051"
---
# <a name="translator-setup-dlls"></a>DLL di installazione del convertitore
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare solo in modo esplicito ODBC nelle versioni precedenti di Windows.  
  
 La DLL di installazione di Translator contiene la funzione **ConfigTranslator** , che restituisce l'opzione predefinita per un convertitore. Se necessario, viene richiesto all'utente di ottenere tali informazioni. Per una descrizione completa di questa funzione, vedere informazioni di [riferimento sull'API DLL di installazione](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 La DLL di installazione del convertitore viene scritta dallo sviluppatore di traduzione. Può far parte della DLL di conversione o di una DLL separata.
