---
title: La registrazione di un oggetto Business personalizzato | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 283e623b045e635ef3165b51270c2a257d7856fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929893"
---
# <a name="registering-a-custom-business-object"></a>Registrazione di un oggetto business personalizzato
Per avviare correttamente un oggetto business personalizzato (con estensione dll o .exe) tramite il server Web, il ProgID dell'oggetto business deve essere immesso nel Registro di sistema come descritto in questa procedura. Questa funzionalità di servizi desktop remoto consente di proteggere la sicurezza del server Web tramite l'esecuzione di eseguibili attendibili.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!NOTE]
>  Per Windows dell'applicazione livello dati, l'oggetto business predefinito e MDAC 2.0 e versioni successive [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), non è registrato per impostazione predefinita durante l'installazione dell'applicazione livello dati MDAC/Windows. Tuttavia, se **RDSServer** è stata registrata come sicuri per l'esecuzione nel computer prima dell'installazione, la voce del Registro di sistema viene mantenuta per la nuova installazione.  
  
### <a name="to-register-a-custom-business-object"></a>Per registrare un oggetto business personalizzato:  
  
1.  Fare clic su **avviare** e quindi fare clic su **eseguire**.  
  
2.  Tipo di **RegEdit** e fare clic su **OK**.  
  
3.  Nell'Editor del Registro di sistema, passare al **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch** chiave del Registro di sistema.  
  
4.  Selezionare il **ADCLaunch** chiave e quindi verso il **modificare**dal menu **New** e fare clic su **chiave**.  
  
5.  Digitare il ProgID dell'oggetto business personalizzato e fare clic su **invio**. Lasciare il **valore** voce vuota.


