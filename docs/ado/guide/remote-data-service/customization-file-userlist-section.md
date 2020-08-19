---
description: Sezione UserList del file di personalizzazione
title: Sezione utenti del file di personalizzazione | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: afdd3560de5ca7e64d8a378f1eca04f875903a06
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452233"
---
# <a name="customization-file-userlist-section"></a>Sezione UserList del file di personalizzazione
La sezione relativa all' **utente** è relativa alla sezione **Connect** con lo stesso parametro dell' *identificatore* di sezione.  
  
 Questa sezione può contenere una *voce di accesso utente*che specifica i diritti di accesso per l'utente specificato ed esegue l'override della *voce di accesso* *predefinita* nella sezione **connessione** corrispondente.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
 Una voce di accesso utente è nel formato seguente:  
  
 _nome utente_**=**   
 **_accessRights_**  
  
|Parte|Descrizione|  
|----------|-----------------|  
|*userName*|*Nome utente* della persona che utilizza la connessione. I nomi utente validi vengono stabiliti con la finestra di dialogo **Service Manager** di IIS.|  
|**_accessRights_**|Uno dei seguenti diritti di accesso:<br /><br /> -   **NoAccess** : l'utente non può accedere all'origine dati.<br />-   **ReadOnly** -l'utente può leggere l'origine dati.<br />-   **ReadWrite** -l'utente può leggere o scrivere nell'origine dati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione connessione file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sezione log file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sezione SQL del file di personalizzazione](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Personalizzazione di datafactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Impostazioni client obbligatorie](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Informazioni sul file di personalizzazione](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Scrittura di un gestore personalizzato](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


