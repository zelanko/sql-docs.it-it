---
title: Uso di Servizi componenti Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91d6dcf0ca7f87d6ed510d582f7a7ba0f80e8c74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088153"
---
# <a name="using-microsoft-component-services"></a>Uso dei Servizi componenti Microsoft
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 È possibile abilitare un database Oracle per l'utilizzo con servizi componenti transazionali (o MTS, se si utilizza Windows NT) in Microsoft Windows NT/Windows 2000 e Microsoft Windows 95/98. Per consentire a un database Oracle di funzionare con servizi componenti che supportano le transazioni, gli amministratori di sistema devono creare una vista denominata V $ XATRANS $. Per creare questo script, è necessario eseguire uno script fornito da Oracle. Per ulteriori informazioni, vedere la Guida di Servizi componenti o la documentazione di Oracle.
