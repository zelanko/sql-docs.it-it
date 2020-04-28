---
title: Impostazione del formato di marshalling del flusso DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29bf8d19b9e3c9ec9b4072edd9575add9947c8f3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922210"
---
# <a name="setting-dcom-stream-marshaling-format"></a>Configurazione del formato di marshalling del flusso DCOM
Un computer client che usa componenti di RDS 1,5 o versione precedente non è compatibile con un server che usa componenti di RDS 2,0 o versione successiva. Quando si utilizza DCOM come protocollo sottostante, il supporto per Servizi Desktop remoto 2,0 o versione successiva è più efficiente per il trasporto di oggetti [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) . Se il client esegue componenti da Servizi Desktop remoto 1,5 o versioni precedenti, è possibile impostare il server in modo che funzioni con il supporto Servizi Desktop remoto precedente (denominato RDS 1,0) o il supporto RDS più recente (denominato RDS 2,0 o versione successiva). Impostare una delle seguenti voci del registro di sistema:  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -oppure-  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```


