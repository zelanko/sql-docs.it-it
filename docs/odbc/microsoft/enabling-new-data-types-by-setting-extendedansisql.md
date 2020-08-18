---
description: Abilitazione di nuovi tipi di dati tramite l'impostazione di ExtendedAnsiSQL
title: Abilitazione di nuovi tipi di dati tramite l'impostazione di ExtendedAnsiSQL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 609fdda7e56fe1c249df26da3f0117aab3634084
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412497"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Abilitazione di nuovi tipi di dati tramite l'impostazione di ExtendedAnsiSQL
Nei database Jet 4,0 sono disponibili due nuovi tipi di dati quando il flag ExtendedAnsiSQL è attivato: SQL_DECIMAL e SQL_NUMERIC. La precisione e la scala predefinite sono rispettivamente 18 e 0. I dati a cui si accede tramite ODBC tipizzati come SQL_DECIMAL o SQL_NUMERIC verranno mappati a Microsoft Jet Decimal anziché alla valuta.  
  
 Quando il flag ExtendedAnsiSQL è disattivato, non è possibile creare tabelle con tipi decimali o numerici e questi tipi non verranno visualizzati in SQLGetTypeInfo (). Tuttavia, se la tabella contiene i nuovi tipi di dati, è possibile utilizzarli con i tipi di dati corretti.
