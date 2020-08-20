---
description: DLL di installazione del convertitore
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
ms.openlocfilehash: 2fe4d514f098773024392666d8f528592d362da4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487394"
---
# <a name="translator-setup-dlls"></a>DLL di installazione del convertitore
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare solo in modo esplicito ODBC nelle versioni precedenti di Windows.  
  
 La DLL di installazione di Translator contiene la funzione **ConfigTranslator** , che restituisce l'opzione predefinita per un convertitore. Se necessario, viene richiesto all'utente di ottenere tali informazioni. Per una descrizione completa di questa funzione, vedere informazioni di [riferimento sull'API DLL di installazione](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 La DLL di installazione del convertitore viene scritta dallo sviluppatore di traduzione. Può far parte della DLL di conversione o di una DLL separata.
