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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b6c99dffc94f2675efdbbc3d5c1d142a5ae9b7e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093846"
---
# <a name="translator-setup-dlls"></a>DLL di installazione del convertitore
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare solo in modo esplicito ODBC nelle versioni precedenti di Windows.  
  
 La DLL di installazione di Translator contiene la funzione **ConfigTranslator** , che restituisce l'opzione predefinita per un convertitore. Se necessario, viene richiesto all'utente di ottenere tali informazioni. Per una descrizione completa di questa funzione, vedere informazioni di [riferimento sull'API DLL di installazione](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 La DLL di installazione del convertitore viene scritta dallo sviluppatore di traduzione. Può far parte della DLL di conversione o di una DLL separata.
