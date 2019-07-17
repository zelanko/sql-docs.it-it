---
title: Configurazione di RDS in Windows 2000 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6230fb7ffbaa1226bc65d391d988ad064617998
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922891"
---
# <a name="configuring-rds-on-windows-2000"></a>Configurazione di RDS in Windows 2000
Se si riscontrano difficoltà nella Guida di servizi desktop remoto funzioni correttamente dopo l'aggiornamento a Windows 2000, seguire questi passaggi per risolvere il problema:  
  
1.  Assicurarsi che il servizio pubblicazione sul Web sia in esecuzione, passare a https:// server con Internet Explorer. Se è Impossibile accedere al server Web in questo modo, aprire un prompt dei comandi e immettere il comando seguente, "NET START W3SVC".  
  
2.  Nel menu Start, scegliere Esegui. Digitare msdfmap e quindi fare clic su OK per aprire il file MSDFMAP nel blocco note. Controllare la sezione [DEFAULT connettersi] e se il parametro di accesso è impostato su NOACCESS, cambiarla in sola lettura.  
  
3.  Tramite l'utilità RegEdit, passare a "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo" e assicurarsi che **HandlerRequired** è impostata su 0 e **DefaultHandler** è "" (stringa Null).  
  
     **Nota** se si apportano modifiche a questa sezione del Registro di sistema, è necessario arrestare e riavviare il servizio pubblicazione sul Web immettendo i comandi seguenti da un prompt dei comandi: "NET STOP W3SVC" e "NET START W3SVC".  
  
4.  Tramite l'utilità RegEdit, passare nel Registro di sistema "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch" e verificare che sia presente una chiave denominata **RDSServer**. In caso contrario, crearla.  
  
5.  Utilizzare Gestione servizi Internet, individuare il sito Web predefinito e visualizzare le proprietà della radice virtuale MSADC. Controllare le Directory sicurezza/indirizzo IP e le restrizioni sul nome di dominio. Se il "accesso negato" è selezionato, quindi selezionare "Granted".  
  
 Assicurarsi di provare a riavviare il server se le modifiche non vengono visualizzati per risolvere il problema a prima.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565). A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows. Eseguire la migrazione di applicazioni che usano servizi desktop remoto [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


