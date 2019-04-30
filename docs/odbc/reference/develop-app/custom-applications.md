---
title: Le applicazioni personalizzate | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ab470951162b5e4035c1253ed4ce425356ad8ec
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042527"
---
# <a name="custom-applications"></a>Applicazioni personalizzate
Le applicazioni personalizzate in genere eseguono un'attività specifica per i pochi DBMS. Ad esempio, un'applicazione può recuperare i dati da un singolo DBMS e generare un report o può trasferire i dati tra diversi DBMS. Ciò che queste applicazioni hanno in comune è che queste DBMS sono noti prima che l'applicazione viene scritta e poco probabile che cambino durante il ciclo di vita dell'applicazione.  
  
 L'applicazione personalizzata richiede pertanto senza alcuna interoperabilità. Lo sviluppatore dell'applicazione è possibile scegliere un singolo driver per ogni sistema DBMS e il codice direttamente per i driver. L'applicazione in modo sicuro può contenere codice specifico del driver per sfruttare le funzionalità di tali driver e può anche effettuare chiamate per le API di database nativo l'utilizzo delle funzionalità non supportate da ODBC.  
  
 Il problema di interoperabilità principali di maggior parte delle applicazioni personalizzate è che il DBMS di destinazione verrà modificato in futuro. In questo caso, questo processo può essere semplificato da cui iniziare la scrittura di codice più interoperabile. Tuttavia, tale modifica del DBMS è rara e in genere comporta una grande quantità di lavoro. Per questo motivo, gli sviluppatori di applicazioni personalizzate raramente scelgono di aumentare l'interoperabilità a scapito della funzionalità. in genere si sceglie di recode tale funzionalità quando vengono modificati DBMS.
