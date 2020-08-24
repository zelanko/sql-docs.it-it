---
description: Configurazione dei server virtuali su IIS
title: Configurazione di server virtuali in IIS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a537ed684fb3f39d89af8c7f95d4e2f1abdb140
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759858"
---
# <a name="configuring-virtual-servers-on-iis"></a>Configurazione dei server virtuali su IIS
Quando si creano server virtuali nella Internet Information Services 4,0, per configurare il server virtuale per l'utilizzo con Servizi Desktop remoto sono necessari i due passaggi aggiuntivi seguenti:  
  
1.  Quando si configura il server, selezionare "Consenti accesso Execute".  
  
2.  Spostare msadcs.dll in *VRoot*\MSADC, dove *VRoot* è la home directory del server virtuale.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](./rds-fundamentals.md)