---
title: Implementare la sicurezza dinamica mediante i filtri di riga | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 715d3b06ed3017a00852f58c618e2ea0b0de24d8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62467915"
---
# <a name="supplemental-lesson---implement-dynamic-security-by-using-row-filters"></a>Lezione supplementare: implementare la sicurezza dinamica mediante i filtri di riga
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione supplementare verrà creato un ruolo aggiuntivo che implementa la sicurezza dinamica. La sicurezza dinamica offre la sicurezza a livello di riga in base al nome o all'ID di accesso dell'utente attualmente connesso. Per altre informazioni, vedere [Ruoli](../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
Per implementare la sicurezza dinamica, è necessario aggiungere una tabella al modello contenente i nomi degli utenti di Windows che possono creare una connessione al modello come origine dati ed esplorare oggetti modello e dati. Il modello creato in questa esercitazione è nel contesto di Adventure Works Corp. Tuttavia, per completare questa lezione, è necessario aggiungere una tabella contenente gli utenti del proprio dominio. Non saranno necessarie le password dei nomi utente che verranno aggiunti. Per creare una tabella EmployeeSecurity con un piccolo campione di utenti del proprio dominio, si userà la funzionalità Incolla e incollare i dati dei dipendenti da un foglio di calcolo di Excel. In uno scenario realistico la tabella che contiene i nomi utente da aggiungere a un modello utilizza in genere una tabella di un database effettivo come origine dati, ad esempio una tabella dimEmployee reale.  
  
Per implementare la sicurezza dinamica, si useranno due nuove funzioni DAX: [Funzione USERNAME (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) e [LOOKUPVALUE (DAX)-funzione](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Queste funzioni applicate in una formula di filtro di riga vengono definite in un nuovo ruolo. Utilizzando la funzione LOOKUPVALUE, la formula specifica un valore dalla tabella EmployeeSecurity e quindi passa che valore alla funzione USERNAME, che specifica il nome utente dell'utente connesso appartiene a questo ruolo. L'utente può quindi esplorare solo i dati specificati dai filtri di riga del ruolo. In questo scenario verrà specificato che i dipendenti addetti alle vendite possono esplorare solo i dati relativi alle vendite Internet per i territori di vendita in cui sono membri.  
  
Per completare questa lezione supplementare, verrà completata una serie di attività. Le attività che sono specifiche di questo scenario di modello tabulare Adventure Works, ma che potrebbero non applicarsi necessariamente a uno scenario realistico, vengono identificate come tali. Ogni attività include informazioni aggiuntive che descrivono lo scopo dell'attività.  
  
Tempo stimato per il completamento della lezione: **30 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento della lezione supplementare fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività di questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti.  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>Aggiungere la tabella dimSalesTerritory al progetto AW Internet Sales Tabular Model  
Per implementare la sicurezza dinamica per questo scenario di Adventure Works, è necessario aggiungere due tabelle aggiuntive al modello. La prima tabella da aggiungere è dimSalesTerritory (come Territorio vendita) dallo stesso database AdventureWorksDW. In un secondo momento si applicherà un filtro di riga alla tabella SalesTerritory che definisce i dati specifici che l'utente connesso può esplorare.  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>Per aggiungere la tabella dimSalesTerritory  
  
1.  In SSDT scegliere il **Model** menu e quindi fare clic su **connessioni esistenti**.  
  
2.  Nella finestra di dialogo **Connessioni esistenti** verificare che sia selezionata la connessione origine dati **Adventure Works DB da SQL** , quindi fare clic su **Apri**.  
  
    Se viene visualizzata la finestra di dialogo credenziali di rappresentazione, digitare le credenziali di rappresentazione usate nella lezione 2: Aggiungere i dati.  
  
3.  Nella pagina **Scelta della modalità di importazione dei dati** lasciare selezionata l'opzione **Seleziona da un elenco di tabelle e viste per scegliere i dati da importare** , quindi fare clic su **Avanti**.  
  
4.  Nella pagina **Seleziona tabelle e viste** selezionare la tabella **DimSalesTerritory** .  
  
5.  Fare clic su **Anteprima e Filtro**.  
  
6.  Deselezionare la colonna **SalesTerritoryAlternateKey** , quindi fare clic su **OK**.  
  
7.  Nella pagina **Seleziona tabelle e viste** fare clic su **Fine**.  
  
    La nuova tabella verrà aggiunta all'area di lavoro del modello. Oggetti e dati dalla tabella di origine DimSalesTerritory vengono quindi importati di AW Internet Sales Tabular Model.  
  
9. Dopo l'importazione della tabella fare clic su **Chiudi**.  

## <a name="add-a-table-with-user-name-data"></a>Aggiungere una tabella con i dati del nome utente  
Poiché nella tabella dimEmployee nel database di esempio AdventureWorksDW sono contenuti utenti del dominio AdventureWorks e i nomi di questi utenti non esistono nel proprio ambiente, è necessario creare una tabella nel modello contenente una piccola parte degli utenti effettivi dell'organizzazione, ad esempio tre utenti. Tali utenti verranno quindi aggiunti come membri al nuovo ruolo. Non sono necessarie le password per i nomi utente di esempio, ma saranno necessari nomi utente di Windows effettivi presenti nel proprio dominio.  
  
#### <a name="to-add-an-employeesecurity-table"></a>Per aggiungere una tabella EmployeeSecurity  
  
1.  Aprire Microsoft Excel creando un nuovo foglio di lavoro.  
  
2.  Copiare la tabella seguente, inclusa la riga di intestazione, quindi incollarla nel foglio di lavoro.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Sostituire il nome, cognome e dominio\nomeutente con i nomi e gli ID di accesso dei tre utenti dell'organizzazione. Inserire lo stesso utente nelle prime due righe per EmployeeId 1. a indicare che tale utente appartiene a più territori di vendita. Lasciare i campi EmployeeId e SalesTerritoryId così come sono.  
  
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
  
1.  In Progettazione modelli in vista diagramma nel **DimGeography** di tabella, fare clic e tenere premuto il **SalesTerritoryId** colonna, quindi trascinare il cursore di **SalesTerritoryId** colonna di **DimSalesTerritory** di tabella e quindi rilasciare.  
  
2.  Nel **FactInternetSales** di tabella, fare clic e tenere premuto il **SalesTerritoryId** colonna, quindi trascinare il cursore il **SalesTerritoryId** colonna il  **DimSalesTerritory** di tabella e quindi rilasciare.  
  
    Si noti che la proprietà attiva per questa relazione è False, ovvero che è inattiva. Questo avviene perché la tabella FactInternetSales include già un'altra relazione attiva utilizzata nelle misure.  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>Nascondere la tabella EmployeeSecurity dalle applicazioni client  
In questa attività si nasconderà la tabella EmployeeSecurity, impedendone la visualizzazione nell'elenco di campi di un'applicazione client. Tenere presente che nascondere una tabella non significa proteggerla. Gli utenti possono comunque recuperare i dati della tabella EmployeeSecurity se sanno come. Per proteggere i dati della tabella EmployeeSecurity, impedendo agli utenti di essere in grado di eseguire una query dei dati, si applicherà un filtro in un'attività successiva.  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>Per nascondere la tabella EmployeeSecurity dalle applicazioni client  
  
-   In Vista diagramma di Progettazione modelli, fare clic con il pulsante destro del mouse sull'intestazione della tabella **Dipendente** , quindi scegliere **Nascondi a strumenti client**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Creare un ruolo utente Addetti alle vendite per territorio  
In questa attività verrà creato un nuovo ruolo utente. Questo ruolo includerà un filtro di riga che definisce le righe della tabella DimSalesTerritory che sono visibili agli utenti. Il filtro viene quindi applicato nella direzione relazione uno-a-molti a tutte le altre tabelle correlate a DimSalesTerritory. Inoltre, si applicherà un semplice filtro che protegge l'intera tabella EmployeeSecurity impedendone da qualsiasi utente membro del ruolo.  
  
> [!NOTE]  
> Il ruolo Addetti alle vendite per territorio creato in questa lezione consente ai membri di esplorare o eseguire query solo sui dati di vendita relativi al territorio di vendita a cui appartengono. Se si aggiunge un utente come membro a addetti alle vendite dal ruolo territorio presente anche come un membro in un ruolo creato nella [lezione 11: Creare ruoli](../analysis-services/lesson-11-create-roles.md), si otterrà una combinazione di autorizzazioni. Se un utente è membro di più ruoli, le autorizzazioni e i filtri di riga definiti per ogni ruolo sono cumulativi, ovvero l'utente disporrà di maggiori autorizzazioni determinate dalla combinazione dei ruoli.  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>Per creare un ruolo utente Addetti alle vendite per territorio  
  
1.  In SSDT scegliere il **modello** menu e quindi fare clic su **ruoli**.  
  
2.  Nelle **gestione ruoli**, fare clic su **New**.  
  
    All'elenco verrà aggiunto un nuovo ruolo con l'autorizzazione Nessuno.  
  
3.  Fare clic sul nuovo ruolo, quindi nella colonna **Nome** rinominare il ruolo in **Addetti alle vendite per territorio**.  
  
4.  Nella colonna **Autorizzazioni** fare clic nell'elenco a discesa, quindi selezionare l'autorizzazione **Lettura**.  
  
5.  Fare clic sulla scheda **Membri** , quindi su **Aggiungi**.  
  
6.  Nel **Seleziona utente o gruppo** nella finestra di dialogo **immettere i nomi degli oggetti da selezionare**, digitare il primo nome utente di esempio usato durante la creazione della tabella EmployeeSecurity. Fare clic su **Controlla nomi** per verificare che il nome utente sia valido, quindi fare clic su **OK**.  
  
    Ripetere questo passaggio, aggiungendo gli altri nomi utente di esempio usato durante la creazione della tabella EmployeeSecurity.  
  
7.  Fare clic sulla scheda **Filtri di riga** .  
  
8.  Per il **EmployeeSecurity** tabella le **filtro DAX** colonna, digitare la formula seguente.  
  
    ```
      =FALSE()  
    ```
  
    Questa formula specifica che tutte le colonne vengono risolte nella condizione booleana; false Pertanto, non le colonne della tabella EmployeeSecurity possono eseguire query da un membro di addetti alle vendite ruolo utente di territorio.  
  
9. Per la tabella **DimSalesTerritory** digitare la formula seguente.  

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
In questa attività si userà l'analizza nella funzionalità di Excel in SSDT per testare l'efficacia di addetti alle vendite per ruolo utente di territorio. Si specificherà uno dei nomi utente che è stato aggiunto alla tabella EmployeeSecurity e come membro del ruolo. Questo nome utente verrà quindi utilizzato come nome utente effettivo nella connessione creata tra Excel e il modello.  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>Per testare il ruolo utente Addetti alle vendite per territorio  
  
1.  In SSDT scegliere il **Model** menu e quindi fare clic su **analizza in Excel**.  
  
2.  Nella finestra di dialogo **Analizza in Excel** in **Specificare il nome utente o il ruolo da usare per la connessione al modello**selezionare **Altro utente di Windows**, quindi fare clic su **Sfoglia**.  
  
3.  Nel **Seleziona utente o gruppo** nella finestra di dialogo **immettere il nome dell'oggetto da selezionare**, digitare uno dei nomi utente inclusi nella tabella EmployeeSecurity e quindi fare clic su **Controlla nomi**.  
  
4.  Fare clic su **OK** per chiudere la finestra di dialogo **Seleziona utente o gruppo** , quindi fare clic su **OK** per chiudere la finestra di dialogo **Analizza in Excel** .  
  
    Verrà aperto Excel con una nuova cartella di lavoro. Viene creata automaticamente una tabella pivot. Elenco PivotTable Fields include la maggior parte dei campi dati disponibili nel nuovo modello.  
  
    La tabella EmployeeSecurity non è visibile nell'elenco PivotTable Fields. in quanto in un'attività precedente si è scelto di nascondere questa tabella agli strumenti client.  
  
5.  Nel **i campi** elenco **∑ Internet Sales** (misure) selezionare il **InternetTotalSales** misure. La misura verrà immessa nei campi **Valori** .  
  
6.  Selezionare il **SalesTerritoryId** colonna il **DimSalesTerritory** tabella. La colonna verrà immessa nei campi **Etichette di riga** .  
  
    Si noti che le cifre delle vendite Internet vengono visualizzate solo per l'area a cui appartiene il nome utente effettivo utilizzato. Se si seleziona un'altra colonna, ad esempio, City, nella tabella DimGeography come campo etichetta di riga, solo le città del territorio di vendita a cui appartiene l'utente effettivo vengono visualizzati.  
  
    Questo utente non può esplorare né eseguire una query sui dati delle vendite Internet per territori diversi da quello a cui appartiene poiché il filtro di riga definito per la tabella Territorio vendita nel ruolo utente Addetti alle vendite per territorio protegge in effetti tutti i dati correlati agli altri territori di vendita.  
  
## <a name="see-also"></a>Vedere anche  
[Funzione USERNAME (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)  
[Funzione LOOKUPVALUE (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)  
[Funzione CUSTOMDATA (DAX)](http://msdn.microsoft.com/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
