---
title: Soluzioni per RDA | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 40485562c8385e05ced033062563d5c5165218de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922170"
---
# <a name="solutions-for-remote-data-access"></a>Soluzioni per RDA (Remote Data Access)
## <a name="the-issue"></a>Il problema  
 ADO consente all'applicazione direttamente accedere a e modificare origini dati (operazione talvolta denominate un sistema a due livelli). Ad esempio, se la connessione all'origine dati che contiene i dati, che è una connessione diretta in un sistema a due livelli.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Tuttavia, è possibile accedere a origini dati indirettamente attraverso un intermediario, ad esempio Microsoft® Internet Information Services (IIS). Questa disposizione è talvolta definita un sistema a tre livelli. IIS è un sistema client/server che offre un modo efficiente per un'applicazione locale o un client richiamare un programma remoto o server, in Internet o intranet. Il programma del server riesce ad accedere all'origine dati e, facoltativamente, elabora i dati acquisiti.  
  
 Pagina Web intranet, ad esempio, contiene un'applicazione scritta in Microsoft® Visual Basic Scripting Edition (VBScript), che si connette a IIS. IIS a sua volta si connette all'origine dati effettiva, recupera i dati, lo elabora in qualche modo e quindi restituisce le informazioni elaborate all'applicazione.  
  
 In questo esempio, l'applicazione mai direttamente connesso all'origine dati; È stato IIS. E IIS accessibili i dati tramite ADO.  
  
> [!NOTE]
>  L'applicazione client/server non deve essere basato su Internet o intranet (vale a dire, basata sul Web)-quanto potrebbe essere costituita esclusivamente da programmi compilati su una rete locale. Tuttavia, il caso tipico è un'applicazione basata sul Web.  
  
 Dato che un controllo visual, ad esempio una griglia, una casella di controllo o un elenco, può usare le informazioni restituite, è necessario usare facilmente le informazioni restituite da un controllo visual.  
  
 Per visualizzare un'interfaccia di programmazione di applicazioni semplice ed efficiente che supporta i sistemi a tre livelli e restituisce informazioni come facilmente come se fosse stato recuperato in un sistema a due livelli. Servizio dati remoto (RDS) è questa interfaccia.  
  
## <a name="the-solution"></a>Soluzione  
 Servizi Desktop remoto consente di definire un modello di programmazione - la sequenza di attività necessarie per accedere e aggiornare un'origine dati - per ottenere l'accesso ai dati tramite un intermediario, ad esempio Internet Information Services (IIS). Il modello di programmazione riepiloga l'intera funzionalità di servizi desktop remoto.  
  
## <a name="see-also"></a>Vedere anche  
 [Modello di programmazione RDS di base](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [Scenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Utilizzo e sicurezza per RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


