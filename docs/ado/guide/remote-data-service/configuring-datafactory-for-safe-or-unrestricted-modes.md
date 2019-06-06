---
title: Configurazione di DataFactory per la modalità sicura o senza restrizioni | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0ee24eb54db193aa16f15f550de66b92cf9b896c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699783"
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>Configurazione di DataFactory per la modalità sicura o senza restrizioni
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Per impostazione predefinita, ADO viene installato con un "sicura" [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) configurazione. La modalità sicura per i componenti Server di servizi desktop remoto indica che si verifica quanto segue:  
  
1.  Gestore di è obbligatorio con il RDSServer (imposto dall'impostazione di una chiave del Registro di sistema).  
  
2.  Il gestore predefinito, MSDFMAP. Handler, viene registrato, presente nell'elenco di gestori sicuri e contrassegnata come gestore predefinito.  
  
3.  File MSDFMAP viene installato nella directory di Windows. È necessario configurare questo file in base alle esigenze, prima di usare servizi desktop remoto in modalità a tre livelli.  
  
 Facoltativamente, è possibile configurare senza restrizioni **DataFactory** installazione. **Data factory** possono essere usati direttamente, senza il gestore personalizzato. Gli utenti possono ancora usare un gestore personalizzato modificando le stringhe di connessione, ma non è obbligatorio. Per altre informazioni sulle implicazioni dell'uso di **RDSServer** oggetti, vedere [protezione di applicazioni di servizi desktop remoto](../../../ado/guide/remote-data-service/securing-rds-applications.md).  
  
 Per configurare le voci del Registro di sistema di gestore per una configurazione sicura è disponibile il file di registro di sistema handsafe. reg. Per eseguire in modalità provvisoria, eseguire handsafe.  
  
 Dopo aver eseguito handsafe. reg, è necessario arrestare e riavviare il servizio pubblicazione sul Web nel server Web digitando i comandi seguenti in una finestra del prompt dei comandi: "NET STOP W3SVC" e "NET START W3SVC".  
  
## <a name="see-also"></a>Vedere anche  
 [Personalizzazione di DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



