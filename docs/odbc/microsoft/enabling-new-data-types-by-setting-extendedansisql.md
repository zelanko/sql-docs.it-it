---
title: L'abilitazione di nuovi tipi di dati tramite l'impostazione di ExtendedAnsiSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80a86ef188796883e76c6d5f6149a3e40afd341b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128002"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Abilitazione di nuovi tipi di dati tramite l'impostazione di ExtendedAnsiSQL
Due nuovi tipi di dati sono disponibili nei database Jet 4.0 quando il flag ExtendedAnsiSQL è attivato: SQL_DECIMAL e SQL_NUMERIC. La precisione predefinita e la scala sono 18 e 0 rispettivamente. Dati accessibili tramite ODBC tipizzata come SQL_DECIMAL o SQL_NUMERIC verranno mappati per Microsoft Jet decimale invece di valuta.  
  
 Quando il flag ExtendedAnsiSQL è disattivato, non è possibile creare tabelle con tipi di dati decimali o numerici e questi tipi non compariranno nella SQLGetTypeInfo(). Tuttavia, se la tabella contiene i nuovi tipi di dati, possono essere utilizzati con i tipi di dati corretto.
