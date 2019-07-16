---
title: Sezione UserList del File di personalizzazione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 558fd9c8379808e6c2f109a9c9584e8831cddd0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922769"
---
# <a name="customization-file-userlist-section"></a>Sezione UserList del file di personalizzazione
Il **userlist** sezione riguarda le **connettersi** sezione con la stessa sezione *identificatore* parametro.  
  
 In questa sezione può contenere un *voce di accesso utente*, che specifica l'accesso i diritti per l'utente specificato ed esegue l'override di *predefinita* *voce di accesso* nel corrispondenti**connettere** sezione.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
 Una voce di accesso utente è nel formato:  
  
 _userName_ **=**    
 **_accessRights_**  
  
|Parte|Descrizione|  
|----------|-----------------|  
|*userName*|Il *nome utente* della persona che utilizza la connessione. I nomi utente validi vengono stabiliti con IIS **Service Manager** finestra di dialogo.|  
|**_accessRights_**|Uno dei seguenti diritti di accesso:<br /><br /> -   **NoAccess** -utente non è possibile accedere all'origine dati.<br />-   **ReadOnly** -l'utente può leggere l'origine dati.<br />-   **Lettura/scrittura** -utente può leggere o scrivere nell'origine dati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione sulla connessione del File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sezione Log File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sezione SQL del File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Personalizzazione di DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Impostazioni Client richieste](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Informazioni sul file di personalizzazione.](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


