---
title: Controlli generali sugli errori | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- general error checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0c9a3425-0a7c-48de-9ff6-73601c26283e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6b7c37febee411571b8ac8316d3800912e35758
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069923"
---
# <a name="general-error-checks"></a>Controlli degli errori generali
Gestione driver verifica un errore generale. Restituisce sempre SQL_ERROR quando viene rilevato l'errore seguente: la funzione deve essere supportata dal driver.
