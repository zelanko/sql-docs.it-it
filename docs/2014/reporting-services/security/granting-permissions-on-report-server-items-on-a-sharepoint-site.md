---
title: Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 0eb2f34a-3643-4b03-81c2-5741ba7ebefd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c9afb10180087998afd0cc891af895a9db669feb
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017262"
---
# <a name="granting-permissions-on-report-server-items-on-a-sharepoint-site"></a>Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] offre caratteristiche di sicurezza predefinite che è possibile usare per concedere l'accesso agli elementi del server di report dai siti e dalle raccolte di SharePoint. Se sono già state assegnate le autorizzazioni agli utenti, questi ultimi potranno accedere alle operazioni e agli elementi del server di report subito dopo la configurazione delle impostazioni per l'integrazione tra [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] e un server di report. È possibile utilizzare le autorizzazioni esistenti per caricare le definizioni dei report e altri documenti, visualizzare report, creare sottoscrizioni e gestire elementi.  
  
 Se non sono state assegnate autorizzazioni oppure non si ha familiarità con le caratteristiche di sicurezza di [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], attenersi alle linee guida seguenti:  
  
1.  Nella documentazione relativa al prodotto [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], leggere le informazioni sulle impostazioni di sicurezza predefinite per i gruppi di SharePoint standard in modo da apprendere come gestire le autorizzazioni e l'accesso degli utenti.  
  
2.  Esaminare l'elenco di autorizzazioni correlato all'accesso alle operazioni e agli elementi del server di report. Per altre informazioni [Utilizzare la sicurezza predefinita di Windows SharePoint Services per gli elementi del server di report](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md).  
  
3.  Assegnare account utente e di gruppo ai gruppi predefiniti di SharePoint.  
  
4.  È eventualmente possibile creare nuovi gruppi e livelli di autorizzazione oppure modificare quelli esistenti per adattare le autorizzazioni di accesso al server a seconda di specifiche esigenze.  
  
 Per utilizzare le funzionalità di sicurezza di [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] con gli elementi del server di report, è necessario che quest'ultimo venga eseguito in modalità integrata SharePoint.  
  
## <a name="about-permissions-permission-levels-and-sharepoint-groups"></a>Informazioni su autorizzazioni, livelli di autorizzazione e gruppi di SharePoint  
 Nell'elenco seguente è disponibile una breve introduzione alle caratteristiche di sicurezza incluse in [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]. Per ulteriori informazioni, vedere la guida e le procedure di Windows SharePoint nel sito di SharePoint in uso.  
  
-   Gli oggetti a sicurezza diretta includono siti, elenchi, raccolte, cartelle e documenti.  
  
-   Le autorizzazioni vengono concesse per consentire l'esecuzione di un'attività specifica. [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] sono disponibili 33 autorizzazioni predefinite che è possibile combinare in un livello di autorizzazione.  
  
-   I livelli di autorizzazione sono costituiti da un set di autorizzazioni che può essere concesso agli utenti o ai gruppi di SharePoint per un oggetto a sicurezza diretta, ad esempio un sito, una raccolta, un elenco, una cartella, un elemento o un documento. È equivalente a una definizione di ruolo in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Sono disponibili cinque livelli di autorizzazione predefiniti. Se necessario, è possibile personalizzarli o crearne di nuovi.  
  
-   Un gruppo di SharePoint è costituito da un gruppo di utenti che è possibile creare in un sito di SharePoint per gestire le autorizzazioni del sito stesso e offrire un elenco di distribuzione tramite posta elettronica per i suoi membri. I gruppi di SharePoint sono costituiti da account utente e di gruppo di Windows oppure da account di accesso utente se si utilizza l'autenticazione basata su form. [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] sono disponibili tre gruppi. Se necessario, è possibile personalizzarli o crearne di nuovi.  
  
-   L'ereditarietà delle autorizzazioni consente di applicare le impostazioni di sicurezza del sito padre a siti, elenchi ed elementi secondari. È possibile utilizzare le autorizzazioni ereditate per accedere agli elementi del server di report archiviati in una raccolta di SharePoint. L'utilizzo dell'ereditarietà delle autorizzazioni e dei gruppi predefiniti di SharePoint consente di semplificare la distribuzione e offre accesso immediato alla maggior parte delle operazioni del server di report.  
  
## <a name="who-sets-permissions"></a>Responsabili dell'impostazione delle autorizzazioni  
 L'amministratore che installa [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], esegue la Configurazione guidata Prodotti e tecnologie SharePoint e crea il sito portale diventa il proprietario predefinito di quest'ultimo. Il proprietario del sito può impostare le autorizzazioni in Amministrazione centrale per una farm o un'applicazione Web di SharePoint autonoma, nonché nel sito principale di ogni applicazione Web di SharePoint. Il proprietario può inoltre designare altri proprietari del sito.  
  
 Nel sito principale di un'applicazione Web di SharePoint, gli amministratori della raccolta siti possono impostare le autorizzazioni per più siti nella gerarchia di questi ultimi. I singoli proprietari del sito possono eseguire le medesime attività relativamente a un sito secondario.  
  
 Gli amministratori del server o di una raccolta siti possono impostare le opzioni che determinano se altri proprietari del sito possono impostare le autorizzazioni. A seconda del livello di autorizzazione di cui si dispone, potrebbe non essere possibile creare o personalizzare i livelli di autorizzazione o i gruppi di SharePoint.  
  
## <a name="using-predefined-sharepoint-groups-and-permission-levels"></a>Utilizzo dei livelli di autorizzazione e dei gruppi di SharePoint predefiniti  
 Nelle indicazioni incluse nella documentazione relativa al prodotto [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] viene consigliato di usare i gruppi di SharePoint standard, ovvero *Proprietari* **nome sito**, *Proprietari* **nome sito**e *Proprietari* **nome sito**, e di assegnare le autorizzazioni a livello di sito. La maggio parte degli utenti a cui vengono assegnate autoizzazioni devono essere membri dei gruppi *Visitatoi* **nome sito** o *Visitatoi* **nome sito** . Le autorizzazioni nel sito padre vengono ereditate in tutta la gerarchia dei siti. È possibile disattivare l'ereditarietà delle autorizzazioni su determinati elementi per i quali è necessario impostare limitazioni.  
  
 Di seguito vengono illustrati i livelli di autorizzazione predefiniti per i gruppi di SharePoint:  
  
-   Il gruppo **Proprietari** dispone di autorizzazioni di controllo completo che consentono di apportare modifiche al contenuto, alle pagine o alle funzionalità del sito. È consigliabile che l'accesso con controllo completo sia limitato agli amministratori del sito.  
  
-   Il gruppo **Membri** dispone di autorizzazioni di collaborazione che consentono di visualizzare pagine, modificare elementi, inviare richieste di approvazione delle modifiche, aggiungere ed eliminare elementi in un elenco.  
  
-   Il gruppo **Visitatori** dispone di autorizzazioni a livello di lettura che consentono ai membri di un gruppo di visualizzare pagine, elementi di elenco e documenti.  
  
 I gruppi di SharePoint dispongono di livelli di autorizzazione che offrono accesso immediato a numerose operazioni del server di report. Se si ritiene che le impostazioni di sicurezza incorporate non offrano il livello di accesso desiderato, è possibile creare livelli di autorizzazione e gruppi personalizzati.  
  
 Per altre informazioni sulle operazioni del server di report supportate tramite le funzionalità di sicurezza predefinite, vedere [Utilizzare la sicurezza predefinita di Windows SharePoint Services per gli elementi del server di report](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md).  
  
 Per utilizzare le caratteristiche di sicurezza incorporate, è necessario assegnare account utente e di gruppo di Windows ai gruppi di SharePoint. Ad eccezione dell'amministratore del server e del proprietario del sito portale, i quali dispongono di accesso automatico a [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] fin dall'installazione del software, a tutti gli altri utenti devono essere concesse le autorizzazioni affinché possano accedere al server.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Utilizzare la sicurezza predefinita di Windows SharePoint Services per gli elementi del server di report](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
 Illustra le modalità di utilizzo dei livelli di autorizzazione e dei gruppi di SharePoint predefiniti per l'accesso agli elementi del server di report.  
  
 [Informazioni di riferimento sulle autorizzazioni relative a elenchi e siti di SharePoint per gli elementi del server di report](sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
 Offre informazioni di riferimento relative a tutte le autorizzazioni dei prodotti SharePoint utilizzabili per accedere alle operazioni del server di report.  
  
 [Impostare le autorizzazioni per le operazioni del server di report in un'applicazione Web di SharePoint](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)  
 Descrive i requisiti di autorizzazione per il reporting ad hoc e suggerisce approcci utili per rendere disponibili le caratteristiche.  
  
 [Confrontare ruoli e attività di Reporting Services con autorizzazioni e gruppi di SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
 Offre un breve riepilogo di confronto tra i gruppi di SharePoint e le definizioni di ruolo predefinite in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Impostare autorizzazioni per gli elementi del server di report in un sito di SharePoint &#40;Reporting Services in modalità integrata SharePoint&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
 Include istruzioni per la creazione di nuovi gruppi di SharePoint provvisti dell'autorizzazione necessaria per avviare Generatore report e impostare la sicurezza degli elementi dei modelli. In questo argomento sono inoltre incluse linee guida generali relative all'impostazione di autorizzazioni personalizzate per uno o più elementi o operazioni del server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare autorizzazioni per gli elementi del server di report in un sito di SharePoint &#40;Reporting Services in modalità integrata SharePoint&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Sicurezza e protezione di Reporting Services](reporting-services-security-and-protection.md)  
  
  
