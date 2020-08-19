---
description: Registrazione di un oggetto business personalizzato
title: Registrazione di un oggetto business personalizzato | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
author: rothja
ms.author: jroth
ms.openlocfilehash: df390d9e02f31913f74b82ed6196bc2442d1591a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452053"
---
# <a name="registering-a-custom-business-object"></a>Registrazione di un oggetto business personalizzato
Per avviare correttamente un oggetto business personalizzato (file con estensione dll o exe) tramite il server Web, è necessario immettere il ProgID dell'oggetto business nel registro di sistema, come illustrato in questa procedura. Questa funzionalità RDS protegge la sicurezza del server Web eseguendo solo file eseguibili approvati.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!NOTE]
>  Per MDAC 2,0 e versioni successive e Windows DAC, l'oggetto business predefinito, [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), non viene registrato per impostazione predefinita durante l'installazione dell'applicazione livello dati MDAC/Windows. Tuttavia, se **RDSServer. DataFactory** è stato registrato come Safe per l'esecuzione nel computer prima dell'installazione, la voce del registro di sistema viene mantenuta per la nuova installazione.  
  
### <a name="to-register-a-custom-business-object"></a>Per registrare un oggetto business personalizzato:  
  
1.  Fare clic sul pulsante **Start** , quindi scegliere **Esegui**.  
  
2.  Digitare **Regedit** e fare clic su **OK**.  
  
3.  Nell'editor del registro di sistema passare alla chiave del registro di sistema **\system\currentcontrolset\services\w3svc\parameters\adclaunch HKEY_LOCAL_MACHINE** .  
  
4.  Selezionare la chiave **ADCLaunch** , scegliere **nuovo** dal menu **modifica**e quindi fare clic su **chiave**.  
  
5.  Digitare il ProgID dell'oggetto business personalizzato e premere **invio**. Lasciare vuota la voce **valore** .


