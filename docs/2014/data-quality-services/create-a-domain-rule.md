---
title: Creare una regola di dominio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.rules.f1
- sql12.dqs.dm.testdomainrule.f1
ms.assetid: 339fa10d-e22c-4468-b366-080c33f1a23f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0e9f04742bbfabcfa0e351f25e9475a8022689e6
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65481037"
---
# <a name="create-a-domain-rule"></a>Creare una regola di dominio
  In questo argomento viene descritto come creare una regola di dominio in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Una regola di dominio è una condizione utilizzata per convalidare, correggere e standardizzare i valori di dominio. Una regola di dominio deve rimanere valida in tutto il dominio affinché i valori di dominio vengano considerati accurati e conformi ai requisiti aziendali. Le regole di dominio possono includere le regole di convalida utilizzate per convalidare i valori di dominio, ma non per correggere i dati in un progetto Data Quality. Le regole includono anche le regole di standardizzazione applicate ai dati validi e utilizzate per la correzione dei dati.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Per creare una regola di dominio, è necessario disporre di una Knowledge Base e di un dominio aperto nell'attività Gestione dominio.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN per creare una regola di dominio.  
  
##  <a name="Build"></a> Compilare le regole di dominio  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire o creare una Knowledge Base. Selezionare **Gestione dominio** come attività, quindi fare clic su **Apri** o **Crea**. Per ulteriori informazioni, vedere [Creare una Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md) o [Apertura di una Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  La gestione del dominio viene eseguita in una pagina del client Data Quality Services che contiene cinque schede per le operazioni di gestione del dominio separate. Non si tratta di un processo basato su procedure guidate. Ciascuna operazione di gestione può essere eseguita separatamente.  
  
3.  Dall'**elenco di domini** nella pagina **Gestione dominio** selezionare il dominio per il quale si desidera creare una regola di dominio o creare un nuovo dominio. Se è necessario creare un nuovo dominio, vedere [Crea un dominio](../../2014/data-quality-services/create-a-domain.md).  
  
4.  Fare clic sulla scheda **Regole di dominio** .  
  
5.  Fare clic su **Aggiungi una nuova regola di dominio**, quindi immettere un nome univoco nella Knowledge Base e una descrizione per la regola.  
  
6.  Selezionare **Attiva** per specificare che la regola verrà eseguita (valore predefinito) o deselezionare per impedire l'esecuzione della regola.  
  
7.  Nel riquadro **Compila una regola** selezionare una condizione dall'elenco a discesa nella casella delle clausole della regola.  
  
8.  Se la condizione richiede un valore, immettere il valore nella casella di testo associata.  
  
9. Fare clic sull'icona **Aggiunge una nuova condizione alla clausola selezionata** se è necessaria un'altra clausola.  
  
10. Selezionare **AND** o **OR** come operatore.  
  
11. Selezionare una condizione dall'elenco a discesa, quindi immettere un valore per l'operando, se necessario.  
  
12. Per modificare l'ordine in cui le clausole vengono visualizzate nell'elenco, selezionare una clausola, quindi fare clic sulla freccia in su o in giù. Verrà modificato l'ordine in cui vengono eseguite le clausole con conseguente effetto sui risultati.  
  
13. Aggiungere ulteriori clausole in base alle esigenze. Se necessario, eliminare una clausola selezionandola e facendo quindi clic su **Elimina la clausola selezionata**.  
  
14. Ripetere le operazioni per aggiungere nuove regole in base alle necessità.  
  
15. Per valutare l'impatto che una regola di convalida avrebbe sui valori se venisse implementata, fare clic sull'icona **Analizza l'impatto della regola di dominio sui valori del dominio** .  
  
16. Continuare con la procedura relativa al test descritta di seguito.  
  
##  <a name="Test"></a> Testare le regole di dominio  
  
1.  Con una regola selezionata fare clic sull'icona **Esegui la regola del dominio selezionato sui dati di test** .  
  
2.  Nella finestra di dialogo Esegui la regola di dominio fare clic sull'icona **Aggiunge un nuovo termine di test per la regola di dominio** . Immettere un valore da testare. Immettere gli altri valori in base alle esigenze. Selezionare un valore e fare clic sull'icona **Rimuovi il termine di test selezionato** , se necessario.  
  
3.  Fare clic sull'icona **Testa la regola di dominio su tutti i termini** .  
  
4.  Controllare la validità di ogni termine. Un segno di spunta significa "corretto", una croce significa "errore" e un triangolo significa "non valido".  
  
5.  Al termine, fare clic su **Chiudi** nella finestra di dialogo del test.  
  
6.  Ripetere le operazioni per altre regole in base alle necessità.  
  
7.  Continuare con la procedura relativa all'applicazione descritta di seguito.  
  
##  <a name="Apply"></a> Applicare le regole di dominio  
  
1.  Fare clic su **Applica tutte le regole** per applicare le regole ai valori nel dominio. Quando si fa clic su **Applica tutte le regole**, viene visualizzata una finestra popup che indica il numero di valori in determinati stati che sarà interessato dalla regola. Fare clic su **Sì** se si desidera comunque applicare la regola oppure su **No** se non si desidera applicarla. Se si sceglie **Sì**, fare clic su **OK** per chiudere la finestra popup dei risultati.  
  
    > [!NOTE]  
    >  Quando si crea o si modifica una regola, non è necessario salvare le modifiche. Tuttavia, è necessario applicare la regola per rendere effettive le modifiche.  
  
2.  Fare clic su **Ignora tutte le modifiche** per rimuovere tutte le modifiche apportate alle regole di dominio ripristinando le regole applicate in precedenza, in modo che tutte le modifiche apportate dopo l'ultima applicazione delle regole non vengano più applicate. La validità di ogni valore nel dominio verrà aggiornata in base alle regole applicate in precedenza e non in base alle modifiche eliminate.  
  
3.  Fare clic su **Fine** per completare l'attività di gestione del dominio, come descritto in [Sospensione dell'attività di gestione del dominio](../../2014/data-quality-services/end-the-domain-management-activity.md).  
  
##  <a name="FollowUp"></a> Completamento: fasi successive alla creazione di una regola di dominio  
 Dopo avere creato una regola di dominio, è possibile eseguire ulteriori attività di gestione del dominio, quali l'individuazione delle informazioni per aggiungere informazioni o l'aggiunta di criteri di corrispondenza al dominio. Per altre informazioni, vedere [Eseguire l'individuazione delle informazioni](../../2014/data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../../2014/data-quality-services/managing-a-domain.md) o [Creare criteri di corrispondenza](../../2014/data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Conditions"></a> Condizioni delle regole di dominio  
 Nella tabella seguente vengono descritte le condizioni che è possibile applicare nella regola di dominio e viene fornito un esempio per illustrare la modalità di applicazione delle condizioni.  
  
 Quando viene applicata una regola di dominio e un valore del dominio non supera la regola, il valore viene definito Non validi. Un valore definito Non validi verrà modificato in Corretti se la regola che fa sì che il valore non sia valido viene eliminata o disattivata oppure se la regola viene modificata affinché il valore superi la regola. Se un valore viene definito Non validi manualmente (nella scheda Valori di dominio dell'attività di gestione del dominio) e la regola che il valore non supera viene eliminata, disattivata o modificata, il valore rimarrà Non validi in base alla designazione manuale.  
  
 Una regola di dominio con una condizione definitiva applicherà la logica delle regole ai sinonimi del valore nella condizione o nelle condizioni, oltre ai valori stessi. Le condizioni definitive sono: Il valore è uguale a, Il valore è diverso da, Il valore è in o Il valore non è in. Si supponga ad esempio di avere la regola di dominio seguente: "Per 'City', il valore è uguale a 'Los Angeles'". Se 'Los Angeles' e 'LA' sono sinonimi, entrambi saranno corretti. Se invece la regola non contiene una condizione definitiva, ad esempio "Per City, il valore termina con "s", "Los Angeles" risulta corretto, mentre il sinonimo "LA" rappresenta un errore.  
  
 Durante la creazione di una regola di dominio è possibile scegliere tra diverse alternative. Ad esempio, per verificare se i valori iniziano con la lettera A, B o C, è possibile creare una regola semplice con una condizione complessa, ad esempio un'espressione regolare con i caratteri barra verticale, oppure è possibile creare una regola complessa che contiene diverse condizioni semplici. Un esempio della prima regola è "Il valore contiene l'espressione regolare (^A|^B|^C)". Un esempio della seconda regola è "'Il valore inizia con A' OR 'Il valore inizia con B' OR 'Il valore inizia con C'".  
  
|Condizione|Descrizione|Esempio|  
|---------------|-----------------|-------------|  
|La lunghezza è uguale a|Solo i valori costituiti dal numero di caratteri definito dall'operando saranno validi.|Operando di esempio: 3<br /><br /> Valore valido: BB1<br /><br /> Valore non valido: AA|  
|La lunghezza è maggiore o uguale a|Solo i valori costituiti dal numero di caratteri definito dall'operando o da un numero di caratteri maggiore saranno validi.|Operando di esempio: 3<br /><br /> Valori validi: BB1, BBAA<br /><br /> Valore non valido: AA|  
|La lunghezza è minore o uguale a|Solo i valori costituiti dal numero di caratteri definito dall'operando o da un numero di caratteri minore saranno validi.|Operando di esempio: 3<br /><br /> Valori validi: BB1, AA<br /><br /> Valore non valido: BBAA|  
|Il valore è uguale a|Solo i valori identici all'operando saranno validi.|Operando di esempio: BB1<br /><br /> Valore valido: BB1<br /><br /> Valore non valido: BB, BB1#|  
|Il valore è diverso da|Solo i valori non identici all'operando saranno validi.|Operando di esempio: BB1<br /><br /> Valore valido: BB, BB1#<br /><br /> Valore non valido: BB1|  
|Il valore contiene|Solo i valori in cui tutti i caratteri sono contenuti all'interno dell'operando, in qualsiasi ordine, saranno validi.|Operando di esempio: A1<br /><br /> Valori validi: A1, AA1<br /><br /> Valore non valido: 1A, AA|  
|Il valore non contiene|Solo i valori non contenuti all'interno dell'operando saranno validi.|Operando di esempio: A1<br /><br /> Valori validi: 1A, AA<br /><br /> Valori non validi: A1, AA1|  
|Il valore inizia con|Solo i valori che iniziano con i caratteri dell'operando saranno validi.|Operando di esempio: AA<br /><br /> Valori validi: AA1<br /><br /> Valori non validi: 1AAB|  
|Il valore termina con|Solo i valori che terminano con i caratteri dell'operando saranno validi.|Operando di esempio: AA<br /><br /> Valori validi: 1AA<br /><br /> Valori non validi: 1AAB|  
|Il valore è numerico|Solo i valori che contengono un tipo di dati numerico di SQL Server saranno validi, ad esempio int, decimal, float, ecc.|Operando di esempio: N/D<br /><br /> Valori validi: 1, 25, 345.1234<br /><br /> Valori non validi: 2b, bcdef|  
|Il valore è data/ora|Solo i valori che contengono un tipo di dati data/ora di SQL Server saranno validi, ad esempio datetime, time, date, ecc.|Operando di esempio: N/D<br /><br /> Valori validi: 06-04-1916; 06-04-1916 18:24:24; 21 marzo 2001; 18/5/2011; 18:24:24<br /><br /> Valori non validi: 213 marzo 2006|  
|Il valore è in|Solo i valori presenti nel set dell'operando saranno validi.<br /><br /> Per immettere i valori nel set, fare clic nella casella di testo dell'operando, immettere il primo valore, premere Invio, immettere il secondo valore, ripetere le operazioni per tutti i valori che si desidera immettere nel set, quindi fare di nuovo clic nella casella di testo dell'operando. In DQS verrà aggiunta una virgola tra i valori nel set. Se si immette una singola stringa con virgole senza ritorno a capo, ad esempio "A1, B1", tale stringa verrà considerata come un singolo valore nel set.|Operando di esempio: [A1, B1]<br /><br /> Valori validi: A1, B1<br /><br /> Valori non validi: AA, 11|  
|Il valore non è in|Solo i valori non presenti nel set dell'operando saranno validi.|Operando di esempio: [A1, B1]<br /><br /> Valori validi: AA, 11<br /><br /> Valori non validi: A1, B1|  
|Il valore corrisponde al modello|Solo i valori che corrispondono al modello di caratteri, cifre o caratteri speciali dell'operando saranno validi.<br /><br /> È possibile usare qualsiasi lettera (A...Z) come modello per qualsiasi lettera, senza distinzione tra maiuscole e minuscole. È possibile usare qualsiasi cifra (0...9) come modello per qualsiasi cifra. Qualsiasi carattere speciale, tranne lettere o cifre, può essere utilizzato come modello per se stesso. Le parentesi quadre, [], definiscono la corrispondenza facoltativa.|Operando di esempio: AA:000 (modello di due caratteri *qualsiasi* seguiti da due punti (:), seguiti da tre cifre *qualsiasi*).<br /><br /> Valori validi: AB:012, df:257<br /><br /> Valori non validi: abc:123, FJ-369<br /><br /> Per ulteriori informazioni sulle regole basate su un modello in DQS e gli esempi, vedere [Ricerche nelle regole di dominio DQS](https://blogs.msdn.com/b/dqs/archive/2012/10/08/pattern-matching-in-dqs-domain-rules.aspx).|  
|Il valore non corrisponde al modello|Solo i valori che non corrispondono al modello di caratteri, cifre o caratteri speciali dell'operando saranno validi.|Operando di esempio: A1 (il valore non deve corrispondere a un modello formato da un carattere *qualsiasi* seguito da una cifra *qualsiasi*).<br /><br /> Valori validi: AB1, A, A:5<br /><br /> Valori non validi: B7, c9|  
|Il valore contiene il modello|Solo i valori che contengono il modello di caratteri, cifre o caratteri speciali dell'operando saranno validi.|Operando di esempio: AA-12 (il valore contiene un modello di due caratteri *qualsiasi* seguiti da un trattino (-), seguito da due cifre *qualsiasi*).<br /><br /> Valori validi: AAA-01, ab-975<br /><br /> Valore non valido: A7, AA-6, C-45, aa;98|  
|Il valore non contiene il modello|Solo i valori che non contengono il modello di caratteri dell'operando saranno validi.|Operando di esempio: AB-12 (il valore non deve contenere un modello di due caratteri *qualsiasi* seguiti da un trattino (-), seguito da due cifre *qualsiasi*).<br /><br /> Valori validi: A7, AA-6, C-45, aa;98<br /><br /> Valore non valido: AAA-01, ab-975|  
|Valore corrispondente a un'espressione regolare|Solo i valori uguali all'espressione regolare dell'operando saranno considerati validi.<br /><br /> Non includere l'ancoraggio "^" o l'ancoraggio "$" nell'espressione regolare perché in DQS tali ancoraggi vengono aggiunti automaticamente a una clausola che contiene la condizione Il valore è uguale all'espressione regolare. In alternativa, è possibile includere l'espressione regolare contenente gli ancoraggi "^" e "$" tra parentesi. Per ulteriori informazioni sulle espressioni regolari, vedere [Elementi del linguaggio di espressioni regolari](https://go.microsoft.com/fwlink/?LinkId=225561).|Operando di esempio: [1-5] + (ogni carattere deve essere una cifra numerica compresa tra 1 e 5, ripetuta una o più volte)<br /><br /> Valori validi: 123, 12345, 14352<br /><br /> Valori non validi: 456, ABC|  
|Valore non corrispondente a un'espressione regolare|Solo i valori che non corrispondono all'espressione regolare dell'operando saranno considerati validi.|Operando di esempio: [1-5] + (la stringa non deve essere costituita solo da cifre numeriche comprese tra 1 e 5)<br /><br /> Valori validi: 456, ABC<br /><br /> Valore non valido: 123, 123456, 14352|  
  
  
