---
title: Configurazione client di Riesecuzione distribuita | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ccf03e32-6bd9-43c0-b9b6-9fe0d9163339
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3eb00922b4f6e21dd4cfc8a46d8c0c27ed9a5be1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095481"
---
# <a name="distributed-replay-client-configuration"></a>Configurazione client Riesecuzione distribuita
  Usare la pagina di **Configurazione client Riesecuzione distribuita** dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per specificare gli utenti a cui si desidera concedere autorizzazioni amministrative per il servizio client Riesecuzione distribuita.  
  
 Gli utenti che dispongono di autorizzazioni amministrative disporranno di accesso illimitato al servizio client Riesecuzione distribuita.  
  
## <a name="options"></a>Opzioni  
 **Nome controller**  
 Si tratta di un parametro facoltativo e il valore predefinito è \< *blank*>.  
  
 Immettere il nome del controller che il computer client comunicherà con per il servizio client Riesecuzione distribuita. Tenere presente quanto segue:  
  
-   Il nome deve essere un nome di dominio completo. Ad esempio, è possibile che un host denominato server1 nella gerarchia dei prodotti di Microsoft disponga di un nome di dominio completo server1.products.microsoft.com.  
  
-   Se è già stato configurato un controller, immettere il nome del controller durante la configurazione di ciascuno client.  
  
-   In caso contrario, è possibile lasciare vuoto il nome del controller. Tuttavia, è necessario immettere manualmente il nome del controller nel file **configurazione client** .  
  
 **Directory di lavoro**  
 Specificare la directory di lavoro per il servizio client Riesecuzione distribuita.  
  
 La directory di lavoro predefinita \<corrisponde alla *lettera di unità*>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:\\\Program Files \DReplayClient\WorkingDir.  
  
 **Directory dei risultati**  
 Specificare la directory dei risultati per il servizio client Riesecuzione distribuita.  
  
 La directory dei risultati predefinita \< *è lettera di unità*>:\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Program\\files \DReplayClient\ResultDir.  
  
  
