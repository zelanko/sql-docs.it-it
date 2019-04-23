---
title: Assegnazioni di ruolo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- users [Reporting Services]
- roles [Reporting Services]
- role-based security [Reporting Services], role assignments
- groups [Reporting Services]
- security [Reporting Services], role assignments
ms.assetid: 600e112c-1897-48a6-93c0-6e9f3f12dc01
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3b9875628e8868e38ed471b15b411eab86bbd1cb
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59969037"
---
# <a name="role-assignments"></a>Assegnazioni di ruolo
  In [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]le *assegnazioni di ruolo* determinano l'accesso agli elementi archiviati e al server di report. Un'assegnazione di ruolo è composta dalle parti seguenti:  
  
-   Un elemento a sicurezza diretta per il quale si desidera controllare l'accesso. Cartelle, report e risorse sono esempi di elementi a sicurezza diretta.  
  
-   Un account utente o di gruppo che può essere autenticato tramite la sicurezza di Windows o un altro meccanismo di autenticazione.  
  
-   Definizioni di ruolo che definiscono un set di attività. Sono esempi di definizioni di ruolo **Amministratore sistema**, **Gestione contenuto**e **Server di pubblicazione**.  
  
 Le assegnazioni di ruolo vengono ereditate all'interno della gerarchia di cartelle. L'assegnazione di ruolo definita per una cartella viene ereditata automaticamente da tutte le origini dei dati condivise, le risorse, le sottocartelle e i report contenuti nella cartella. Per i singoli elementi, è possibile definire assegnazioni di ruolo che avranno la priorità su quelle ereditate. Ogni parte della gerarchia di cartelle deve essere protetta da almeno un'assegnazione di ruolo. Non è possibile creare un elemento senza sicurezza né modificare le impostazioni in modo che un elemento rimanga senza sicurezza.  
  
 Nella figura seguente è illustrata un'assegnazione di ruolo in cui viene eseguito il mapping di un gruppo e di un utente specifico al ruolo **Server di pubblicazione** per la cartella B.  
  
 ![Diagramma di assegnazioni dei ruoli](../media/report-securityarch.gif "Diagramma di assegnazioni dei ruoli")  
Diagramma di assegnazione dei ruoli  
  
## <a name="system-level-and-item-level-role-assignments"></a>Assegnazioni di ruolo a livello di sistema e di elemento  
 In [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] la sicurezza basata sui ruoli è organizzata nei livelli seguenti:  
  
-   Le assegnazioni di ruolo a livello di elemento controllano l'accesso ai report, alle cartelle, ai modelli di report, alle origini dei dati condivise e alle risorse nella gerarchia di cartelle del server di report. Le assegnazioni di ruolo a livello di elemento vengono definite quando si crea un'assegnazione di ruolo su un'elemento specifico o sulla cartella Home.  
  
-   Le assegnazioni di ruolo a livello di sistema autorizzano operazioni che sono definite a livello di ambito sul server nel suo complesso, ad esempio la capacità di gestire i processi è un'operazione a livello di sistema. Un'assegnazione di ruolo a livello di sistema non equivale a un amministratore di sistema. Non conferisce autorizzazioni avanzate che concedono il controllo totale di un server di report.  
  
 Un'assegnazione di ruolo a livello di sistema non autorizza l'accesso agli elementi nella gerarchia di cartelle. La sicurezza a livello di sistema e la sicurezza a livello di elemento si escludono a vicenda. Per offrire un accesso sufficiente a un server di report per un utente o un gruppo, potrebbe essere necessario creare un'assegnazione di ruolo sia a livello di sistema che di elemento.  
  
## <a name="users-and-groups-in-role-assignments"></a>Utenti e gruppi nelle assegnazioni di ruolo  
 Gli account utente o di gruppo che vengono specificati nelle assegnazioni di ruolo sono account di dominio. Il server di report fa riferimento a utenti e gruppi di un dominio [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows o di un altro modello di sicurezza se si usa un'estensione di sicurezza personalizzata, ma non crea né gestisce utenti e gruppi.  
  
 Non possono esistere assegnazioni di ruolo diverse applicate allo stesso elemento che specificano lo stesso utente o gruppo. Se un account utente è anche membro di un account di gruppo e a entrambi sono associate assegnazioni di ruolo, per l'utente saranno disponibili le attività selezionate per entrambe le assegnazioni di ruolo.  
  
 Quando si aggiunge un utente a un gruppo che fa già parte di un'assegnazione di ruolo, è necessario reimpostare Internet Information Services (IIS) affinché l'assegnazione di ruolo diventi effettiva per l'utente.  
  
## <a name="predefined-role-assignments"></a>Assegnazioni di ruolo predefinite  
 Per impostazione predefinita, vengono implementate assegnazioni di ruolo predefinite che consentono agli amministratori locali di gestire il server di report. Per consentire l'accesso ad altri utenti è necessario specificare assegnazioni di ruolo aggiuntive.  
  
 Per altre informazioni sulle assegnazioni di ruolo predefinite che forniscono sicurezza predefinita, vedere [Ruoli predefiniti](role-definitions-predefined-roles.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creare, eliminare o modificare un ruolo &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)   
 [Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](grant-user-access-to-a-report-server.md)   
 [Modificare o eliminare un'assegnazione di ruolo &#40;Gestione report&#41;](role-assignments-modify-or-delete.md)   
 [Impostare autorizzazioni per gli elementi del server di report in un sito di SharePoint &#40;Reporting Services in modalità integrata SharePoint&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](granting-permissions-on-a-native-mode-report-server.md)  
  
  
