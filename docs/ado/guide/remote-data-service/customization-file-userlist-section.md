---
description: Sezione UserList del file di personalizzazione
title: Sezione utenti del file di personalizzazione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: b09e5f9356ad196e03c970623369d4918a6f5506
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724752"
---
# <a name="customization-file-userlist-section"></a>Sezione UserList del file di personalizzazione
La sezione relativa all' **utente** è relativa alla sezione **Connect** con lo stesso parametro dell' *identificatore* di sezione.  
  
 Questa sezione può contenere una *voce di accesso utente*che specifica i diritti di accesso per l'utente specificato ed esegue l'override della *voce di accesso* *predefinita* nella sezione **connessione** corrispondente.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintassi  
 Una voce di accesso utente è nel formato seguente:  
  
 _nome utente_**=**   
 **_accessRights_**  
  
|Parte|Descrizione|  
|----------|-----------------|  
|*userName*|*Nome utente* della persona che utilizza la connessione. I nomi utente validi vengono stabiliti con la finestra di dialogo **Service Manager** di IIS.|  
|**_accessRights_**|Uno dei seguenti diritti di accesso:<br /><br /> -   **NoAccess** : l'utente non può accedere all'origine dati.<br />-   **ReadOnly** -l'utente può leggere l'origine dati.<br />-   **ReadWrite** -l'utente può leggere o scrivere nell'origine dati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione connessione file di personalizzazione](./customization-file-connect-section.md)   
 [Sezione log file di personalizzazione](./customization-file-logs-section.md)   
 [Sezione SQL del file di personalizzazione](./customization-file-sql-section.md)   
 [Personalizzazione di datafactory](./datafactory-customization.md)   
 [Impostazioni client obbligatorie](./required-client-settings.md)   
 [Informazioni sul file di personalizzazione](./understanding-the-customization-file.md)   
 [Scrittura di un gestore personalizzato](./writing-your-own-customized-handler.md)