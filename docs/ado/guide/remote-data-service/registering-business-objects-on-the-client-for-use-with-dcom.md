---
description: Registrazione degli oggetti business sul client per l'uso con DCOM
title: Registrazione di oggetti business sul client per l'utilizzo con DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
author: rothja
ms.author: jroth
ms.openlocfilehash: fa974d7c0f495639f576604933fc0ce10fd4451f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452043"
---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>Registrazione degli oggetti business sul client per l'uso con DCOM
Per gli oggetti business personalizzati è necessario assicurarsi che il lato client sia in grado di eseguire il mapping del nome del programma (ProgId) a un identificatore (CLSID) che può essere utilizzato su DCOM. Per questo motivo, il ProgID dell'oggetto DCOM deve trovarsi nel registro di sistema sul lato client ed eseguire il mapping all'ID classe dell'oggetto business sul lato server. Per gli altri protocolli supportati (HTTP, HTTPS e in-process), questa operazione non è necessaria.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Se, ad esempio, si espone un oggetto business sul lato server denominato MyBObj con un ID di classe specifico, ad esempio, "{00112233-4455-6677-8899-00AABBCCDDEE}", assicurarsi che le voci seguenti vengano aggiunte al registro di sistema sul lato client:  
  
```console
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```


