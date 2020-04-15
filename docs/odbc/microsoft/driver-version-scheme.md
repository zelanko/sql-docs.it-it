---
title: Schema di versione del driver Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 864a8bd892315b060fc6fcf42dbe69dfea61ae59
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303452"
---
# <a name="driver-version-scheme"></a>Schema delle versioni del driver
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Nella tabella seguente sono elencate tutte le versioni rilasciate di Driver Microsoft ODBC per Oracle.  
  
|Versione driver|Numero di build|Cronologia disponibilità|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C'è 4.2 e Visual Basic 5.0, Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 e MDAC 1.5a|  
|2.0 aggiornato|2.73.7283.01|IIS 4.0|  
|2.0 aggiornato|2.73.7283.03|MDAC 1.5b e 1.5c|  
|2.0 aggiornato|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 e MDAC 2.0|  
|2.5 aggiornato|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 Build 2.00.6235 (versione 1) è stata la prima versione del driver Microsoft ODBC per Oracle. Dopo il rilascio della prima versione, è stata adottata una nuova convenzione di denominazione.  
  
 Ad esempio, 2.73.7283.03 può essere suddiviso nei seguenti componenti distinti:  
  
-   2 - Il numero di versione.  
  
-   73 - La versione di Oracle Server per cui è stato progettato il driver.  
  
-   7283.03 - Il numero di build del driver.  
  
> [!NOTE]  
>  Con la versione 2.573.2973, la convenzione di denominazione ha creato una certa confusione sul fatto che 2.573 è una versione precedente rispetto alla versione 2.73, ma ogni sezione del numero di build deve essere considerata singolarmente. Il numero 573 è maggiore di 73, quindi è una versione più recente. Inoltre, "2.5" indica il numero di versione del driver.
