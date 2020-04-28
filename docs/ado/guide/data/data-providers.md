---
title: Provider di dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 40506ec971782c5e9108a34fd240faabcc2756b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925653"
---
# <a name="data-providers"></a>Provider di dati
I provider di dati rappresentano diverse origini di dati, ad esempio database SQL, file indicizzati sequenziali, fogli di calcolo, archivi di documenti e file di posta elettronica. I provider espongono i dati in modo uniforme usando un'astrazione comune denominata set di righe.  
  
 ADO è potente e flessibile perché può connettersi a uno dei diversi provider di dati e comunque esporre lo stesso modello di programmazione, indipendentemente dalle funzionalità specifiche di un determinato provider. Tuttavia, poiché ogni provider di dati è univoco, il modo in cui l'applicazione interagisce con ADO varierà in base al provider di dati.  
  
 Ad esempio, le funzionalità e le funzionalità del provider OLE DB per SQL Server, che viene utilizzato per accedere ai database Microsoft SQL Server, sono notevolmente diverse da quelle del provider Microsoft OLE DB per Internet Publishing, che viene utilizzato per accedere agli archivi di file in un server Web.
