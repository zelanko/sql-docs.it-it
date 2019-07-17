---
title: Schema della versione del driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d8a155f5d76e8a250c64d3d59e160fbb5863414f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071853"
---
# <a name="driver-version-scheme"></a>Schema delle versioni del driver
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 La tabella seguente elenca tutte le versioni rilasciate di Microsoft ODBC Driver per Oracle.  
  
|Versione del driver|Numero di build|Cronologia disponibilità|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 e Visual Basic 5.0, Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 e MDAC 1,5 a|  
|2.0 aggiornata|2.73.7283.01|IIS 4.0|  
|2.0 aggiornata|2.73.7283.03|MDAC 1.5b e 1.5 c|  
|2.0 aggiornata|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 e MDAC 2.0|  
|2.5 aggiornato|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 Compilazione 2.00.6235 (versione 1) viene eseguita la prima versione di Microsoft ODBC Driver per Oracle. Dopo il rilascio della prima versione, è stata adottata una convenzione di denominazione di nuovo.  
  
 Ad esempio, 2.73.7283.03 può suddividere i seguenti componenti distinti:  
  
-   2 = il numero di versione.  
  
-   73 = la versione del Server Oracle per il quale è stato progettato il driver.  
  
-   7283.03 = il numero di build del driver.  
  
> [!NOTE]  
>  Con la versione 2.573.2973, la convenzione di denominazione ha portato a qualche confusione che 2.573 è una versione precedente rispetto a 2,73, ma ogni sezione del numero di build deve essere considerate singolarmente. Il numero 573 è maggiore di 73, pertanto è una versione più recente. Inoltre, "2.5" indica il numero di versione del driver.
