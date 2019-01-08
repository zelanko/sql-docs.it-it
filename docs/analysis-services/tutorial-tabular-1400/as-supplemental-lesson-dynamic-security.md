---
title: "Analysis Services lezione supplementare dell'esercitazione: La sicurezza dinamica | Microsoft Docs"
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: 4abe105c2bb083ba4479d4d23418e0e73adce5f7
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398429"
---
# <a name="supplemental-lesson---dynamic-security"></a>Lezione supplementare - Sicurezza dinamica

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione supplementare si crea un ruolo aggiuntivo che implementa la sicurezza dinamica. La sicurezza dinamica offre la sicurezza a livello di riga in base al nome o all'ID di accesso dell'utente attualmente connesso. 
  
Per implementare la sicurezza dinamica, è aggiungere una tabella al modello contenente i nomi degli utenti che possono connettersi al modello ed esplorare dati e oggetti modello. Il modello creato in questa esercitazione è nel contesto di Adventure Works; Tuttavia, per completare questa lezione, è necessario aggiungere una tabella contenente gli utenti del proprio dominio. Non è necessaria la password per i nomi utente aggiunti. Per creare una tabella EmployeeSecurity con un piccolo campione di utenti del proprio dominio, è usare la funzionalità Incolla e incollare i dati dei dipendenti da un foglio di calcolo di Excel. In uno scenario reale, la tabella contenente i nomi utente in genere sarebbe una tabella di un database effettivo come un'origine dati. ad esempio, una tabella DimEmployee reale.  
  
Per implementare la sicurezza dinamica, si usano due funzioni DAX: [Funzione USERNAME (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) e [LOOKUPVALUE (DAX)-funzione](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Queste funzioni applicate in una formula di filtro di riga vengono definite in un nuovo ruolo. Usando la funzione LOOKUPVALUE, la formula specifica un valore dalla tabella EmployeeSecurity. La formula passa quindi che valore alla funzione USERNAME, che specifica il nome utente dell'utente connesso appartiene a questo ruolo. L'utente può quindi esplorare solo i dati specificati dai filtri di riga del ruolo. In questo scenario, si specifica che i dipendenti possono esplorare solo i dati di vendite Internet per i territori di vendita in cui sono membri.  
  
Le attività che sono specifiche di questo scenario di modello tabulare Adventure Works, ma che potrebbero non applicarsi necessariamente a uno scenario realistico, vengono identificate come tali. Ogni attività include informazioni aggiuntive che descrivono lo scopo dell'attività.  
  
Tempo stimato per il completamento della lezione: **30 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  

Questo articolo lezione supplementare fa parte di un'esercitazione di modellazione tabulare, che deve essere completata nell'ordine. Prima di eseguire le attività di questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti.  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>Aggiungere la tabella dimSalesTerritory al progetto AW Internet Sales Tabular Model  

Per implementare la sicurezza dinamica per questo scenario di Adventure Works, è necessario aggiungere due tabelle aggiuntive al modello. La prima tabella da aggiungere è DimSalesTerritory (come territorio vendita) dallo stesso database AdventureWorksDW. In un secondo momento si applica un filtro di riga alla tabella SalesTerritory che definisce i dati specifici che l'utente connesso può esplorare.  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>Per aggiungere la tabella dimSalesTerritory  
  
1.  In Esplora modelli tabulari > **Zdroje dat**, fare doppio clic la connessione e quindi fare clic su **Importa nuove tabelle**.  

    Se viene visualizzata la finestra di dialogo credenziali di rappresentazione, digitare le credenziali di rappresentazione usate nella lezione 2: Aggiungere i dati.
  
2.  Nel Pannello di navigazione selezionare la **DimSalesTerritory** tabella e quindi fare clic su **OK**.    
  
3.  Fare clic nell'Editor di Query, il **DimSalesTerritory** eseguire una query e quindi rimuovere **SalesTerritoryAlternateKey** colonna.  
  
7.  Fare clic su **Importa**.  
  
    La nuova tabella viene aggiunta all'area di lavoro modello. Oggetti e dati dalla tabella di origine DimSalesTerritory vengono quindi importati di AW Internet Sales Tabular Model.  
  
9. Dopo la tabella è stata importata correttamente, fare clic su **Chiudi**.  

## <a name="add-a-table-with-user-name-data"></a>Aggiungere una tabella con i dati del nome utente  

La tabella DimEmployee nel database di esempio AdventureWorksDW contiene utenti del dominio AdventureWorks. Tali nomi utente non esistono nel proprio ambiente. È necessario creare una tabella nel modello che contenga un piccolo campione (almeno tre) di utenti effettivi dell'organizzazione. Aggiungere quindi gli utenti come membri al nuovo ruolo. Non è necessaria la password per i nomi utente di esempio, ma è necessario nomi utente di Windows effettivi presenti nel proprio dominio.  
  
#### <a name="to-add-an-employeesecurity-table"></a>Per aggiungere una tabella EmployeeSecurity  
  
1.  Aprire Microsoft Excel per creare un foglio di lavoro.  
  
2.  Copiare la tabella seguente, inclusa la riga di intestazione, quindi incollarla nel foglio di lavoro.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Sostituire il nome, cognome e dominio\nomeutente con i nomi e gli ID di accesso dei tre utenti dell'organizzazione. Inserire lo stesso utente nelle prime due righe per EmployeeId 1, indicare che l'utente appartiene a più di un territorio di vendita. Lasciare i campi EmployeeId e SalesTerritoryId così come sono.  
  
4.  Salvare il foglio di lavoro **SampleEmployee**.  
  
5.  Nel foglio di lavoro, selezionare tutte le celle con i dati dei dipendenti, incluse le intestazioni, quindi fare doppio clic su dati selezionati e quindi fare clic su **copia**.  
  
6.  In SSDT scegliere il **Edit** menu e quindi fare clic su **Incolla**.  
  
    Se Incolla è disattivato, fare clic su qualsiasi colonna di qualsiasi tabella nella finestra di progettazione modelli e ripetere l'operazione.  
  
7.  Nel **anteprima Incolla** nella finestra di dialogo **Table_name**, tipo **EmployeeSecurity**.  
  
8.  Nelle **dati da incollare**, verificare che i dati includano tutti i dati utente e le intestazioni dal foglio di lavoro SampleEmployee.  
  
9. Verificare che l'opzione **Utilizza la prima riga per le intestazioni di colonna** sia selezionata, quindi fare clic su **OK**.  
  
    Viene creata una nuova tabella denominata EmployeeSecurity con i dati dei dipendenti copiati dal foglio di lavoro SampleEmployee.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Creare relazioni tra la tabella FactInternetSales, DimGeography e DimSalesTerritory  

La tabella FactInternetSales, DimGeography e DimSalesTerritory contengono una colonna comune, SalesTerritoryId. La colonna SalesTerritoryId nella tabella DimSalesTerritory contiene i valori con un Id diverso per ogni territorio di vendita.  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a>Per creare relazioni tra il FactInternetSales, DimGeography e dimsalesterritory  
  
1.  In vista diagramma nel **DimGeography** tabella, fare clic e tenere premuto il **SalesTerritoryId** colonna, quindi trascinare il cursore la **SalesTerritoryId** colonna il **DimSalesTerritory** di tabella e quindi rilasciare.  
  
2.  Nel **FactInternetSales** di tabella, fare clic e tenere premuto il **SalesTerritoryId** colonna, quindi trascinare il cursore il **SalesTerritoryId** colonna il  **DimSalesTerritory** di tabella e quindi rilasciare.  
  
    Si noti che la proprietà attiva per questa relazione è False, ovvero che è inattiva. La tabella FactInternetSales include già un'altra relazione attiva.  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>Nascondere la tabella EmployeeSecurity dalle applicazioni client  

In questa attività è nascondere la tabella EmployeeSecurity, impedendone la visualizzazione nell'elenco di campi di un'applicazione client. Tenere presente che nascondere una tabella non significa proteggerla. Gli utenti possono comunque recuperare i dati della tabella EmployeeSecurity se sanno come. Per proteggere i dati della tabella EmployeeSecurity, impedendo agli utenti di essere in grado di eseguire una query dei dati, si applica un filtro in un'attività successiva.  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>Per nascondere la tabella EmployeeSecurity dalle applicazioni client  
  
-   In Vista diagramma di Progettazione modelli, fare clic con il pulsante destro del mouse sull'intestazione della tabella **Dipendente** , quindi scegliere **Nascondi a strumenti client**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Creare un ruolo utente Addetti alle vendite per territorio  

In questa attività si creerà un ruolo utente. Questo ruolo include un filtro di riga che definisce le righe della tabella DimSalesTerritory che sono visibili agli utenti. Il filtro viene quindi applicato nella direzione relazione uno-a-molti a tutte le altre tabelle correlate a DimSalesTerritory. È inoltre possibile applicare un filtro che protegge l'intera tabella EmployeeSecurity impedendone da qualsiasi utente membro del ruolo.  
  
> [!NOTE]  
> Il ruolo Addetti alle vendite per territorio creato in questa lezione consente ai membri di esplorare o eseguire query solo sui dati di vendita relativi al territorio di vendita a cui appartengono. Se si aggiunge un utente come membro a addetti alle vendite dal ruolo territorio presente anche come un membro in un ruolo creato nella [lezione 11: Creare ruoli](../tutorial-tabular-1400/as-lesson-11-create-roles.md), si ottiene una combinazione di autorizzazioni. Se un utente è membro di più ruoli, le autorizzazioni e i filtri di riga definiti per ogni ruolo sono cumulativi, Vale a dire, l'utente dispone delle autorizzazioni maggiori determinate dalla combinazione dei ruoli.  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>Per creare un ruolo utente Addetti alle vendite per territorio  
  
1.  In SSDT scegliere il **modello** menu e quindi fare clic su **ruoli**.  
  
2.  Nelle **gestione ruoli**, fare clic su **New**.  
  
    All'elenco verrà aggiunto un nuovo ruolo con l'autorizzazione Nessuno.  
  
3.  Fare clic sul nuovo ruolo e quindi il **nome** colonna, rinominare il ruolo **Sales Employees by Territory**.  
  
4.  Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa, quindi selezionare l'autorizzazione **Lettura** .  
  
5.  Scegliere il **membri** scheda e quindi fare clic su **Add**.  
  
6.  Nel **Seleziona utente o gruppo** nella finestra di dialogo **immettere i nomi degli oggetti da selezionare**, digitare il primo nome utente di esempio usato durante la creazione della tabella EmployeeSecurity. Fare clic su **Controlla nomi** per verificare che il nome utente sia valido, quindi fare clic su **OK**.  
  
    Ripetere questo passaggio, aggiungendo gli altri nomi utente di esempio usato durante la creazione della tabella EmployeeSecurity.  
  
7.  Scegliere il **filtri di riga** scheda.  
  
8.  Per il **EmployeeSecurity** tabella le **filtro DAX** colonna, digitare la formula seguente:  
  
    ```
      =FALSE()  
    ```
  
    Questa formula specifica che tutte le colonne vengono risolte nella condizione booleana false. Nessuna colonna della tabella EmployeeSecurity può eseguire query da un membro di addetti alle vendite ruolo utente di territorio.  
  
9. Per il **DimSalesTerritory** table, digitare la formula seguente:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    In questa formula la funzione LOOKUPVALUE restituisce tutti i valori per la colonna DimEmployeeSecurity [SalesTerritoryId], in cui EmployeeSecurity [LoginId] corrisponde a quello attualmente connesso in nome utente di Windows ed EmployeeSecurity [SalesTerritoryId] è la uguale a DimSalesTerritory [SalesTerritoryId].  
  
    Il set del territorio di vendita gli ID restituiti da LOOKUPVALUE viene quindi utilizzato per limitare le righe visualizzate nella tabella DimSalesTerritory. Vengono visualizzate solo le righe in cui si trova il valore SalesTerritoryID per la riga nel set di ID restituito dalla funzione LOOKUPVALUE.  
  
10. In Gestione ruoli fare clic su **accettabile**.  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>Testare il ruolo utente Addetti alle vendite per territorio  

In questa attività si userà l'analizza nella funzionalità di Excel in SSDT per verificare l'efficacia di addetti alle vendite per ruolo utente di territorio. Specificare uno dei nomi utente che è stato aggiunto alla tabella EmployeeSecurity e come membro del ruolo. Questo nome utente viene quindi utilizzato come nome utente effettivo nella connessione creata tra Excel e il modello.  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>Per testare il ruolo utente Addetti alle vendite per territorio  
  
1.  In SSDT scegliere il **Model** menu e quindi fare clic su **analizza in Excel**.  
  
2.  Nella finestra di dialogo **Analizza in Excel** in **Specificare il nome utente o il ruolo da usare per la connessione al modello**selezionare **Altro utente di Windows**, quindi fare clic su **Sfoglia**.  
  
3.  Nel **Seleziona utente o gruppo** nella finestra di dialogo **immettere il nome dell'oggetto da selezionare**, digitare un nome utente incluso nella tabella EmployeeSecurity e quindi fare clic su **Controlla nomi**.  
  
4.  Fare clic su **OK** per chiudere la finestra di dialogo **Seleziona utente o gruppo** , quindi fare clic su **OK** per chiudere la finestra di dialogo **Analizza in Excel** .  
  
    Verrà visualizzata la finestra di Excel con una nuova cartella di lavoro. Viene creata automaticamente una tabella pivot. Elenco PivotTable Fields include la maggior parte dei campi dati disponibili nel nuovo modello.  
  
    La tabella EmployeeSecurity non è visibile nell'elenco PivotTable Fields. È stata nascosta dagli strumenti client in un'attività precedente.  
  
5.  Nel **i campi** elenco **∑ Internet Sales** (misure) selezionare il **InternetTotalSales** misure. La misura verrà immessa nel **valori** campi.  
  
6.  Selezionare il **SalesTerritoryId** colonna il **DimSalesTerritory** tabella. La colonna viene inserita il **etichette di riga** campi.  
  
    Si noti che le cifre delle vendite Internet vengono visualizzate solo per l'area a cui appartiene il nome utente effettivo utilizzato. Se si seleziona un'altra colonna, ad esempio City nella tabella DimGeography come campo etichetta di riga, vengono visualizzate solo le città del territorio di vendita a cui appartiene l'utente effettivo.  
    Questo utente non è possibile esplorare o eseguire query sui dati delle vendite Internet per territori diversi da quello che a cui appartengono. Questa restrizione è perché il filtro di riga definito per la tabella DimSalesTerritory, nel ruolo Sales Employees by Territory utente, protegge tutti i dati correlati ad altri territori di vendita.  
  
## <a name="see-also"></a>Vedere anche  

[Funzione USERNAME (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[Funzione LOOKUPVALUE (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[Funzione CUSTOMDATA (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  
