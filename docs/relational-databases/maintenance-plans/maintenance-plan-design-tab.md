---
title: Piano di manutenzione (scheda Progettazione) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.maintplanproperties.optimizations.f1
- sql13.swb.maint.planeditor.f1
- sql13.swb.maint.subplaneditor.f1
ms.assetid: 6d20d4d4-5b3f-454a-8a05-f0aac803c5ad
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1bffeed97e9c56420750ce022c4fa5ec0a56f574
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85666979"
---
# <a name="maintenance-plan-design-tab"></a>Piano di manutenzione (scheda Progettazione)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Usare la finestra di dialogo **Piano di manutenzione (scheda Progettazione)** per specificare le proprietà di un piano di manutenzione e dei relativi sottopiani. Trascinare le attività dalla casella degli strumenti nella finestra di progettazione dei piani di manutenzione. Fare clic con il pulsante destro del mouse su gruppi di attività per creare percorsi di esecuzione con diramazioni. I piani di manutenzione vengono salvati come pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eseguiti da processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opzioni  
 **Aggiungi sottopiano**  
 Consente di aggiungere un sottopiano configurabile.  
  
 **Proprietà sottopiano**  
 Visualizza la finestra di dialogo **Proprietà sottopiano** . Selezionare un sottopiano nella griglia e fare clic su questa icona per immettere il nome, la descrizione e la pianificazione per il sottopiano. È anche possibile fare doppio clic sul sottopiano nella griglia per visualizzare la finestra di dialogo **Proprietà sottopiano** . Per i nomi di sottopiano è previsto un limite di 128 caratteri e per le descrizioni un limite di 512 caratteri.  
  
 **Elimina sottopiano selezionato**  
 Consente di eliminare il sottopiano selezionato.  
  
 **Pianificazione sottopiano**  
 Visualizza la finestra di dialogo **Proprietà pianificazione processo** . Selezionare un sottopiano nella griglia e fare clic su questa icona per configurare una pianificazione per il sottopiano.  
  
 **Rimuovi pianificazione**  
 Consente di rimuovere una pianificazione dal sottopiano selezionato.  
  
 **Gestire le connessioni**  
 Visualizza la finestra di dialogo **Gestisci connessioni** . Questa finestra di dialogo viene utilizzata per aggiungere ulteriori connessioni a istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al piano di manutenzione. Le attività di manutenzione nell'editor sottopiani possono utilizzare una qualsiasi di queste connessioni. Durante l'esecuzione, il piano di manutenzione stabilisce una connessione dal server del piano di manutenzione ai server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificati utilizzando le credenziali di connessione.  
  
 **Report e registrazione**  
 Visualizza la finestra di dialogo **Report e registrazione** usata per gestire report riguardanti l'attività del piano di manutenzione e per configurare la registrazione nel server locale o in un server remoto.  
  
 **Server**  
 Visualizza la finestra di dialogo **Server** usata per selezionare i server in cui verranno eseguite le attività del sottopiano. Questa opzione è abilitata solo nei server master in ambienti multiserver. Per altre informazioni, vedere [Creare un ambiente multiserver](../../ssms/agent/create-a-multiserver-environment.md).  
  
 **Nome**  
 Consente di visualizzare il nome del piano di manutenzione. Il nome dei nuovi piani di manutenzione viene indicato in una finestra di dialogo visualizzata prima dell'apertura della finestra di progettazione dei piani di manutenzione. Per rinominare un piano di manutenzione, fare clic con il pulsante destro del mouse sul piano in Esplora oggetti e quindi scegliere **Rinomina**.  
  
 **Descrizione**  
 Consente di visualizzare o specificare una descrizione per il piano di manutenzione. La lunghezza massima consentita per una descrizione è 512 caratteri.  
  
 **Area di progettazione**  
 Consente di progettare e gestire i piani di manutenzione. Utilizzare l'area di progettazione per aggiungere attività di manutenzione a un piano, rimuovere attività da un piano, specificare collegamenti di precedenza tra le attività e indicare le diramazioni e i parallelismi delle attività.  
  
 Un collegamento di precedenza tra due attività stabilisce una relazione tra le attività. La seconda attività, ovvero *l'attività dipendente*, viene eseguita solo se il risultato dell'esecuzione della prima attività, ovvero *l'attività precedente*, soddisfa i criteri specificati. In genere, il risultato dell'esecuzione è **Esito positivo**, **Esito negativo**o **Completamento**. L'area di progettazione del piano di manutenzione è basata sull'area di progettazione di [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Per altre informazioni, vedere [Vincoli di precedenza](../../integration-services/control-flow/precedence-constraints.md).  
  
 Ad esempio, è possibile specificare che un'attività Deframmenta indice venga eseguita solo dopo il corretto completamento di una precedente attività Controlla integrità database. La caratteristica di collegamento delle precedenze tra le attività consente inoltre la gestione degli errori o delle condizioni di errore all'interno di un piano. Ad esempio, è possibile specificare che, in caso di esito negativo di un'attività Controlla integrità database, all'utente o all'operatore venga trasmessa la notifica dell'errore tramite un'attività Notifica operatore.  
  
 L'impostazione di attività da eseguire quando un'attività precedente non riesce rappresenta un esempio di *diramazione delle attività*.  
  
 L'indicazione di eseguire contemporaneamente due o più attività, ad esempio subito dopo il completamento di un'attività precedente, rappresenta un esempio di *parallelismo delle attività*. Tutte le attività senza vincoli verranno avviate ed eseguite in parallelo. Utilizzare i vincoli per ritardare le attività in modo che le attività precedenti vengano completate per prime.  
  
 Dopo aver posizionato un'attività di manutenzione sull'area di progettazione, sarà possibile modificarne le proprietà in base alle esigenze. Ad esempio, il database specifico di cui eseguire il backup in un'Attività Backup database viene specificato dopo aver aggiunto l'attività al piano. Le attività non correttamente configurate presenti sull'area di progettazione contengono un'icona rossa con una X bianca.  
  
 Per aggiungere un'attività di manutenzione a un piano, trascinare l'icona dell'attività dalla casella degli strumenti **Attività piano di manutenzione** all'area di progettazione del piano oppure fare doppio clic sull'attività nella casella degli strumenti per aggiungere l'attività all'area di progettazione attiva. Se la casella degli strumenti **Attività piano di manutenzione** non è visualizzata, scegliere **Casella degli strumenti** dal menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Visualizza**di**. Espandere il nodo **Attività piano di manutenzione** nel riquadro **Casella degli strumenti** .  
  
 Per rimuovere un'attività da un piano, selezionare l'attività nell'area di progettazione e premere **CANC** oppure fare clic con il pulsante destro del mouse sull'attività e quindi scegliere **Elimina**.  
  
 Per impostare collegamenti di precedenza tra due attività, trascinare innanzitutto le attività nell'area di progettazione, quindi fare clic sull'attività che deve essere eseguita per prima (attività precedente) e trascinare la freccia sull'attività dipendente. Dopo aver stabilito un collegamento di precedenza, nella finestra di progettazione viene visualizzata una freccia che collega le due attività, con l'attività precedente che punta all'attività dipendente. Per impostazione predefinita, quando viene stabilito per la prima volta un collegamento, il vincolo del collegamento viene impostato in modo che l'attività dipendente venga eseguita solo se il risultato dell'esecuzione dell'attività precedente è **Esito positivo**.  
  
 Per modificare le proprietà di un collegamento di precedenza, fare doppio clic sul collegamento per avviare **Editor vincoli di precedenza**. In questo editor sono disponibili diverse opzioni che consentono di specificare le condizioni logiche che determinano l'esecuzione dell'attività dipendente. Ad esempio, è possibile impostare il **risultato dell'esecuzione** su **Esito negativo**, nel qual caso l'attività dipendente viene eseguita solo se l'attività precedente non riesce. È anche possibile modificare la proprietà del risultato dell'esecuzione di un collegamento in **Esito positivo**, **Esito negativo**o **Completamento**facendo clic con il pulsante destro del mouse sul collegamento e scegliendo un'opzione dal menu di scelta rapida.  
  
 Per specificare la diramazione delle attività, creare innanzitutto collegamenti di precedenza tra due attività. Sull'area di progettazione posizionare quindi un'altra attività dipendente che verrà eseguita in base a risultati diversi rispetto alla prima attività dipendente. Fare clic sull'attività precedente e quindi trascinare la seconda freccia dall'attività precedente all'attività dipendente. Per modificare il risultato dell'esecuzione,**Esito positivo**, **Esito negativo**o **Completamento**, che causa l'esecuzione di un'attività dipendente, fare doppio clic sulla freccia del collegamento e modificare il campo **Risultati esecuzione** . In alternativa, fare clic con il pulsante destro del mouse sul collegamento e scegliere il valore del risultato dell'esecuzione desiderato dal menu di scelta rapida.  
  
 Per specificare il parallelismo delle attività, collegare due o più attività dipendenti a una singola attività precedente. Modificare le proprietà dei collegamenti di precedenza in modo che i collegamenti che puntano alle attività dipendenti che vengono eseguite in parallelo abbiano lo stesso valore nei relativi campi del risultato dell'esecuzione.  
  
## <a name="additional-features-available-from-the-shortcut-menu"></a>Caratteristiche aggiuntive disponibili nel menu di scelta rapida  
 Per visualizzare le opzioni aggiuntive, selezionare una o più attività nell'area di progettazione e quindi fare clic con il pulsante destro del mouse per aprire il menu di scelta rapida. Oltre alle normali opzioni **Taglia**, **Copia**, **Incolla**, **Elimina**e **Seleziona tutto**, per alcune attività sono disponibili le opzioni speciali seguenti.  
  
 **Aggiungi annotazione**  
 Consente di aggiungere una nota descrittiva all'area di progettazione.  
  
 **Modifica**  
 Consente di aprire la finestra di dialogo delle proprietà per l'attività.  
  
 **Disable**  
 Gli oggetti non saranno quindi temporaneamente disponibili.  
  
 **Abilitazione**  
 Consente di ripristinare un'attività disabilitata.  
  
 **Gruppo**  
 Consente di creare un gruppo che contiene una o più attività.  
  
 **Separa**  
 Consente di rimuovere attività da un gruppo.  
  
 **Ridimensiona automaticamente**  
 Consente di impostare le dimensioni di ogni attività sulle dimensioni ottimali per l'attività specifica.  
  
 **Collapse**  
 Consente di nascondere attività all'interno di un gruppo.  
  
 **Espandi**  
 Consente di visualizzare le attività di un gruppo nascoste in precedenza con il comando **Comprimi**.  
  
 **Zoom**  
 Consente di modificare le dimensioni delle attività nell'area di progettazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Piani di manutenzione](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Creare un piano di manutenzione](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
  
