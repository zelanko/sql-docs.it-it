---
title: Assegnazioni di ruolo | Microsoft Docs
ms.date: 05/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
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
ms.openlocfilehash: a6fe3c0cd82d8ee8b92948d76d4f7cdb5fa4cf73
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570563"
---
# <a name="role-assignments"></a>Assegnazioni di ruolo

In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]le *assegnazioni di ruolo* determinano l'accesso agli elementi archiviati e al server di report. Un'assegnazione di ruolo è composta dalle parti seguenti:  
  
- Un elemento a sicurezza diretta per il quale si desidera controllare l'accesso. Cartelle, report e risorse sono esempi di elementi a sicurezza diretta.  
  
- Un account utente o di gruppo che può essere autenticato tramite la sicurezza di Windows o un altro meccanismo di autenticazione.  
  
- Le definizioni di ruolo definiscono un set di attività consentite e includono:
  - **Browser**
  - **Gestione contenuto**
  - **Report personali**
  - **Server di pubblicazione**
  - **Generatore report**
  - **Amministratore sistema**
  - **Utente sistema**

 Le assegnazioni di ruolo vengono ereditate all'interno della gerarchia di cartelle e sono automaticamente ereditate dagli elementi contenuti seguenti:

- **Report**
- **Origini dati condivise**
- **Risorse**
- **Sottocartelle**

Per i singoli elementi, è possibile definire assegnazioni di ruolo che avranno la priorità su quelle ereditate. Ogni parte della gerarchia di cartelle deve essere protetta da almeno un'assegnazione di ruolo. Non è possibile creare un elemento non protetto né modificare le impostazioni in modo da ottenerne uno.  
  
 Nella figura seguente è illustrata un'assegnazione di ruolo in cui viene eseguito il mapping di un gruppo e di un utente specifico al ruolo **Server di pubblicazione** per la cartella B.  
  
 ![Diagramma di assegnazioni dei ruoli](../../reporting-services/security/media/report-securityarch.gif "Diagramma di assegnazioni dei ruoli")  
Diagramma di assegnazione dei ruoli  
  
## <a name="system-level-and-item-level-role-assignments"></a>Assegnazioni di ruolo a livello di sistema e di elemento

 In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] la sicurezza basata sui ruoli è organizzata nei livelli seguenti:

- Le assegnazioni di ruolo a livello di elemento controllano l'accesso agli elementi nella gerarchia di cartelle del server di report, ad esempio:
  - report
  - cartelle
  - Modelli di report
  - origini dati condivise
  - altre risorse

- Le assegnazioni di ruolo a livello di elemento vengono definite quando si crea un'assegnazione di ruolo per un elemento specifico o per la cartella Home.

- Le assegnazioni di ruolo a livello di sistema autorizzano operazioni che hanno come ambito l'intero server. La possibilità di gestire processi, ad esempio, è un'operazione a livello di sistema. Un'assegnazione di ruolo a livello di sistema non equivale a un amministratore di sistema. Non conferisce autorizzazioni avanzate che concedono il controllo completo di un server di report.

Un'assegnazione di ruolo a livello di sistema non autorizza l'accesso agli elementi nella gerarchia di cartelle. La sicurezza a livello di sistema e la sicurezza a livello di elemento si escludono a vicenda. Per offrire un accesso sufficiente per un utente o un gruppo, potrebbe talvolta essere necessario creare un'assegnazione di ruolo sia a livello di sistema che a livello di elemento.

## <a name="users-and-groups-in-role-assignments"></a>Utenti e gruppi nelle assegnazioni di ruolo

 Gli account utente o di gruppo che vengono specificati nelle assegnazioni di ruolo sono account di dominio. Il server di report fa riferimento agli utenti e ai gruppi di un dominio [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (o di un altro modello di sicurezza se si usa un'estensione di sicurezza personalizzata), ma non li crea né li gestisce.

Non possono esistere assegnazioni di ruolo diverse applicate allo stesso elemento che specificano lo stesso utente o gruppo. Se un account utente è anche membro di un account di gruppo e a entrambi sono associate assegnazioni di ruolo, per l'utente saranno disponibili le attività selezionate per entrambe le assegnazioni di ruolo.

Quando si aggiunge un utente a un gruppo che ha già un'assegnazione di ruolo, per rendere effettiva la nuova assegnazione di ruolo è necessario reimpostare Internet Information Services (IIS).

## <a name="predefined-role-assignments"></a>Assegnazioni di ruolo predefinite

 Per impostazione predefinita, vengono implementate assegnazioni di ruolo predefinite che consentono agli amministratori locali di gestire il server di report. È possibile aggiungere altre assegnazioni di ruolo per consentire l'accesso ad altri utenti.

 Per altre informazioni sulle assegnazioni di ruolo predefinite che forniscono sicurezza predefinita, vedere [Ruoli predefiniti](../../reporting-services/security/role-definitions-predefined-roles.md).  

## <a name="see-also"></a>Vedere anche

 [Creare, eliminare o modificare un ruolo &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)

 [Modificare o eliminare un'assegnazione di ruolo &#40;portale Web SSRS&#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)

 [Impostare autorizzazioni per gli elementi del server di report in un sito di SharePoint &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)

 [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
