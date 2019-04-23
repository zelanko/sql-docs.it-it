---
title: Memorizzare nella cache le opzioni di aggiornamento (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 05f2cdfc40c8677bfa38c821cfd849c3ce483c31
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59964197"
---
# <a name="cache-refresh-options-report-manager"></a>Opzioni di aggiornamento Cache (Gestione report)
  La pagina Opzioni di aggiornamento cache consente di creare pianificazioni per precaricare nella cache copie temporanee di dati per un report o per un set di dati condiviso. Un piano di aggiornamento include una pianificazione e l'opzione per specificare o eseguire l'override di valori per i parametri. Per un set di dati condiviso, non è possibile eseguire l'override di valori per i parametri contrassegnati di sola lettura. È possibile creare e utilizzare più piani di aggiornamento come parte delle opzioni di aggiornamento.  
  
 Le assegnazioni di ruolo predefinite che consentono di aggiungere, eliminare, modificare e visualizzare report correlati e set di dati condivisi per i piani di aggiornamento della cache sono Gestione contenuto, Report personali e Server di pubblicazione.  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="to-open-the-cache-refresh-plan-properties-page-for-a-report-or-shared-dataset"></a>Per aprire la pagina delle proprietà Piano di aggiornamento della cache per un report o un set di dati condiviso  
  
1.  Aprire Gestione report, quindi individuare il report o il set di dati condiviso per il quale si desidera configurare le proprietà del piano di aggiornamento della cache.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Nell'elenco a discesa fare clic su **Gestisci**. Verrà visualizzata la pagina delle proprietà **Generale** .  
  
4.  Fare clic sulla scheda **Piano di aggiornamento della cache** .  
  
5.  Per creare un nuovo piano della cache, fare clic su **Nuovo piano di aggiornamento della cache**.  
  
    > [!NOTE]  
    >  Per creare un piano di aggiornamento della cache, è necessario abilitare e avviare il servizio SQL Server Agent.  
  
6.  Per creare una copia di un piano della cache e personalizzarlo, fare clic su **Nuovo da esistente.**  
  
## <a name="cache-refresh-options"></a>Opzioni di aggiornamento della cache  
 **Elimina**  
 Consente di eliminare tutti i piani di aggiornamento selezionati.  
  
 **Nuovo da esistente**  
 Questa opzione viene abilitata quando si seleziona un solo piano di aggiornamento della cache. Consente di creare un nuovo piano di aggiornamento copiato dal piano originale. La pagina del piano di aggiornamento della cache viene aperta con i dettagli dal piano selezionato. È possibile modificare le opzioni del piano di aggiornamento e salvare il piano con una nuova descrizione.  
  
 **Nuovo piano di aggiornamento della cache**  
 Fare clic per creare un nuovo piano di aggiornamento da utilizzare nelle opzioni correnti di aggiornamento della cache.  
  
 **Modifica**  
 Selezionare questa opzione per modificare il piano di aggiornamento corrente.  
  
## <a name="cache-refresh-plan-options"></a>Opzioni relative al piano di aggiornamento della cache  
 **Descrizione**  
 Specificare una descrizione per il piano di aggiornamento della cache.  
  
 **Pianificazione specifica dell'elemento**  
 Selezionare questa opzione per creare una pianificazione da utilizzare solo in base a questo elemento.  
  
 **Configurare**  
 Fare clic per aprire la pagina Pianificazione, nella quale è possibile impostare i criteri di frequenza.  
  
 Per altre informazioni, vedere [nuova pianificazione: Pagina di modifica pianificazione &#40;gestione Report&#41;](../../2014/reporting-services/new-schedule-edit-schedule-page-report-manager.md).  
  
 **pianificazione condivisa**  
 Selezionare questa opzione per scegliere una pianificazione esistente.  
  
 Per altre informazioni, vedere [Create, Modify, and Delete Schedules](subscriptions/create-modify-and-delete-schedules.md).  
  
 **@\<** *Parametro* **>**  
 Specificare una combinazione di valori dei parametri. Questa sezione viene visualizzata solo se nel set di dati o nel report corrente sono presenti parametri.  
  
 Vedere [Specifica dei parametri](#Parameters) nella sezione seguente.  
  
 **Utilizzare l'impostazione predefinita**  
 Selezionare questa opzione per utilizzare il valore predefinito per questo parametro.  
  
##  <a name="Parameters"></a> Specificare i parametri  
 Per creare un piano di aggiornamento della cache, a ogni parametro del report o del set di dati condiviso deve essere associato un valore. Se nella definizione dell'elemento del report o del set di dati condiviso non è specificato alcun valore predefinito, è necessario specificarne uno. Se un valore predefinito esiste, non è necessario specificarne alcuno. Se si specifica un valore, quest'ultimo esegue l'override del valore predefinito.  
  
 Per specificare più combinazioni di valori dei parametri, è necessario creare un piano di aggiornamento della cache separato per ogni combinazione.  
  
 Aggiunte, modifiche ed eliminazioni eseguite sui parametri in un report oppure in un set di dati condiviso può influire sul piano di aggiornamento della cache. Se si aggiunge un parametro con un valore predefinito per un report, si rimuove un parametro o si modifica il tipo di dati o l'opzione di sola lettura per un parametro del set di dati condiviso, le modifiche avranno effetto alla successiva elaborazione del piano di aggiornamento della cache.  
  
### <a name="shared-dataset-parameters"></a>Parametri dei set di dati condivisi  
 Per un set di dati condiviso, le informazioni seguenti derivano dalla definizione del set di dati condiviso:  
  
-   **Nome** Specifica il nome del parametro della query.  
  
-   **Tipo** Specifica il tipo di dati di un parametro della query. Poiché questo tipo di dati è sconosciuto fino a quando il provider di dati non elabora la query del set di dati, la convalida del tipo di dati non può essere eseguita fino a quando il set di dati condiviso non è stato elaborato.  
  
-   **Valori Null ammessi** Specifica se NULL è un valore valido.  
  
-   **Di sola lettura** Specifica se questo parametro è contrassegnato come parametro di sola lettura nella definizione del set di dati condiviso. I parametri di sola lettura non vengono visualizzati nell'elenco di parametri per le opzioni di aggiornamento della cache e devono disporre di un'impostazione predefinita specificata come parte della definizione del set di dati condiviso.  
  
-   **Valori predefiniti** I valori predefinito specificati nella definizione del set di dati condiviso. I parametri della query possono essere multivalore. Per eseguire l'override dei valori predefiniti, digitare i nuovi valori nelle aree apposite della casella di testo.  
  
 Se nella definizione del set di dati condiviso viene specificata l'opzione **Ometti dalla query** per un parametro, non è necessario fornire un valore predefinito. Questo flag indica che il parametro del set di dati non è utilizzato nella query. Il parametro viene ad esempio visualizzato nella definizione del set di dati condiviso perché è un parametro del report utilizzato solo nel filtro del set di dati.  
  
 Per visualizzare o modificare opzioni del parametro di set di dati, è necessario modificare la definizione del set di dati condiviso. Per altre informazioni, vedere [Gestire set di dati condivisi](report-data/manage-shared-datasets.md).  
  
### <a name="report-parameters"></a>Parametri report  
 Per creare correttamente un piano di aggiornamento della cache, ogni valore dei parametri del parametro deve essere valido. È necessario digitare o selezionare un valore predefinito per ogni parametro del report. Il valore che si imposta esegue l'override del valore predefinito specificato per il parametro del report sul server di report.  
  
 I parametri devono rispettare i requisiti specificati nelle proprietà relative nel server di report. Ad esempio, se la proprietà AllowBlank è false per un parametro di report, una stringa vuota non è un valore valido.  
  
 Per visualizzare o modificare le opzioni relative ai parametri del report, è necessario modificare i parametri nel report o, in modo indipendente, nel server di report. Per altre informazioni, vedere [concetto dei parametri di Report &#40;Generatore Report e SSRS&#41;](report-design/report-parameters-concepts-report-builder-and-ssrs.md).  
  
## <a name="conditions-that-cause-a-cache-refresh-plan-to-be-inactive"></a>Condizioni che provocano l'inattività di un piano di aggiornamento della cache  
 Le condizioni seguenti possono provocare l'inattività di un set di dati condiviso o di un piano di aggiornamento della cache del report.  
  
-   La cache del set di dati condivisa o l'opzione relativa alla cache del report è disabilitata.  
  
-   I valori obbligatori per il parametro non sono definiti o validi né sono presenti. Prima che il report venga elaborato, è necessario che tutte le query siano valide. Per un report in cui sono presenti sottoreport, tutte le query del set di dati, inclusi i set di dati per il sottoreport, vengono prima elaborate. Se un set di dati non può essere elaborato correttamente, non è possibile eseguire il report.  
  
## <a name="conditions-that-cause-a-cache-refresh-plan-to-be-reactivated"></a>Condizioni che provocano la riattivazione di un piano di aggiornamento della cache  
 Se un piano è inattivo, eseguire una delle operazioni seguenti per attivare la valutazione di un piano di aggiornamento della cache:  
  
-   Modificare un'opzione per il piano.  
  
-   Abilitare la memorizzazione nella cache per un set di dati condiviso associato al piano di aggiornamento.  
  
-   Deselezionare o selezionare l'opzione di sola lettura per un parametro della query del set di dati associato al piano di aggiornamento, quindi salvare la nuova definizione nel server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività a livello di elemento](security/tasks-and-permissions-item-level-tasks.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Guida F1 di gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Memorizzazione dei report nella cache &#40;SSRS&#41;](report-server/caching-reports-ssrs.md)   
 [Gestire set di dati condivisi](report-data/manage-shared-datasets.md)  
  
  
