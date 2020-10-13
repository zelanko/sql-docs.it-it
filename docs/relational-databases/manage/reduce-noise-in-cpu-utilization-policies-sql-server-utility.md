---
title: Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU (utilità SQL Server) | Microsoft Docs
description: Visualizzare le strategie per ridurre le segnalazioni non significative e le violazioni indesiderate nei risultati di Utilità SQL Server. Vedere quali opzioni dei criteri influiscono sui report di utilizzo del processore.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.SWB.UE.ReduceNoise.F1
ms.assetid: 94bf4d93-c0ff-4869-bde7-80c24866092e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 97e37ced535863dfe232fb1299be70774643c1c7
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91811045"
---
# <a name="reduce-noise-in-cpu-utilization-policies-sql-server-utility"></a>Riduzione delle segnalazioni non significative nei criteri di utilizzo della CPU (Utilità SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Utilizzare le strategie seguenti per ridurre le segnalazioni non significative e le violazioni indesiderate dei criteri di utilizzo delle risorse di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-overutilized"></a>Frequenza di violazione dei criteri di utilizzo del processore prima che venga segnalato un sovrautilizzo  
 Il periodo di tempo di valutazione e la tolleranza per le violazioni percentuali sono configurabili utilizzando le impostazioni della scheda **Criteri** nel nodo **Amministrazione utilità** di Esplora utilità. Per modificare i criteri, utilizzare i dispositivi di scorrimento a destra delle descrizioni dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   L'intervallo di raccolta dei dati è impostato su 15 minuti. Questo valore non è configurabile.  
  
-   La soglia superiore predefinita per i criteri di utilizzo del processore è 70%. I valori validi sono compresi tra 0% e 100%.  
  
-   Il periodo di valutazione predefinito per il sovrautilizzo del processore è 1 ora. I valori validi sono compresi tra 1 ora e 1 settimana.  
  
-   La percentuale predefinita di punti dati in violazione prima che venga segnalato un sovrautilizzo della CPU è 20%. I valori validi sono compresi tra 0% e 100%.  
  
 Ad esempio, se si utilizzano i valori predefiniti, 4 punti dati saranno raccolti ogni ora e la soglia dei criteri sarà 20%. Pertanto, per impostazione predefinita, qualsiasi violazione in un periodo di raccolta di 1 ora sarà il 25% di 4 punti dati. I valori predefiniti segnalano qualsiasi violazione della soglia dei criteri di sovrautilizzo della CPU.  
  
 Per ridurre le segnalazioni non significative generate da una sola violazione, considerare le opzioni seguenti:  
  
-   Aumentare il periodo di valutazione di un incremento a 6 ore. Una sola violazione in 6 ore sarebbe 1 punto dati in una dimensione di esempio di 24. In questo caso, i criteri tollererebbero 4 violazioni della soglia dei criteri (16,7% dei punti dati) in 6 ore, ma segnalerebbero un sovrautilizzo per 5 o più violazioni (>20% dei punti dati) in un periodo di raccolta di 6 ore.  
  
-   Aumentare la tolleranza per le violazioni percentuale di un incremento al 30%. Una sola violazione in 1 ora sarebbe 1 punto dati in una dimensione di esempio di 4. In questo caso, i criteri tollererebbero 1 violazione all'ora, ma segnalerebbero un sovrautilizzo per 2 o più violazioni (>30% dei punti dati) in un periodo di raccolta di 1 ora.  
  
-   Aumentare le soglie dei criteri per l'utilizzo del processore da parte dell'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dell'applicazione del livello dati. Per altre informazioni su come modificare i criteri di utilizzo della CPU globali per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o applicazioni livello dati, vedere [Amministrazione utilità &#40;Utilità SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130)). Per altre informazioni su come modificare i criteri di utilizzo della CPU per le singole istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Dettagli di istanze gestite &#40;Utilità SQL Server&#41;](./utility-explorer-f1-help.md). Per altre informazioni su come modificare i criteri di utilizzo della CPU per le singole applicazioni livello dati, vedere [Dettagli di Applicazioni di livello dati distribuite &#40;Utilità SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130)).  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-underutilized"></a>Frequenza di violazione dei criteri di utilizzo del processore prima che venga segnalato un sottoutilizzo  
 Il periodo di tempo di valutazione e la tolleranza per le violazioni percentuali sono configurabili utilizzando le impostazioni della scheda **Criteri** nel nodo **Amministrazione utilità** di Esplora utilità. Per modificare i criteri, utilizzare i dispositivi di scorrimento a destra delle descrizioni dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   L'intervallo di raccolta dei dati è impostato su 15 minuti. Questo valore non è configurabile.  
  
-   La soglia inferiore predefinita per i criteri di utilizzo del processore è 0%. I valori validi sono compresi tra 0% e 100%.  
  
-   Il periodo di valutazione predefinito per il sottoutilizzo del processore è 1 settimana. I valori validi sono compresi tra 1 giorno e 1 mese.  
  
-   La percentuale predefinita di punti dati in violazione prima che venga segnalato un sottoutilizzo della CPU è 90%. I valori validi sono compresi tra 0% e 100%.  
  
 Se si utilizzano i valori predefiniti, ogni settimana vengono raccolti 672 punti dati, ma la soglia dei criteri è 0%. Pertanto, per impostazione predefinita, questi criteri non generano violazioni di sottoutilizzo del processore. Per altre informazioni su come modificare i criteri di utilizzo della CPU globali per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o applicazioni livello dati, vedere [Amministrazione utilità &#40;Utilità SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130)). Per altre informazioni su come modificare i criteri di utilizzo della CPU per le singole istanze di SQL Server, vedere [Dettagli di istanze gestite &#40;Utilità SQL Server&#41;](./utility-explorer-f1-help.md). Per altre informazioni su come modificare i criteri di utilizzo della CPU per le singole applicazioni livello dati, vedere [Dettagli di Applicazioni di livello dati distribuite &#40;Utilità SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130)).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione utilità &#40;Utilità SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130))   
 [Monitoraggio di istanze di SQL Server in Utilità SQL Server](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Modificare una definizione dei criteri di integrità delle risorse &#40;Utilità SQL Server&#41;](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)   
 [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
