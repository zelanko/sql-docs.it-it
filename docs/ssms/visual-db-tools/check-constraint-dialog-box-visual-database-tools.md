---
title: Finestra di dialogo Vincoli CHECK
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraint
ms.assetid: ad0bbf7f-b0de-406a-bd0a-cb779816b101
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: cdcfe6cd4f0c48a6774b8e2518968b8c3d1997f2
ms.sourcegitcommit: e914effe771a1ee323bb3653626cd4ba83d77308
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/04/2020
ms.locfileid: "78280925"
---
# <a name="check-constraint-dialog-box-visual-database-tools"></a>Finestra di dialogo Vincoli CHECK (Visual Database Tools)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Questa finestra di dialogo viene visualizzata facendo clic con il pulsante destro del mouse sulla griglia della definizione di una tabella in Progettazione tabelle e scegliendo **Vincoli CHECK**. In tale finestra di dialogo è contenuto un set di proprietà relative ai vincoli non univoci associati alle tabelle del database. Le proprietà relative ai vincoli univoci invece vengono visualizzate nella finestra di dialogo **Indici/chiavi** .  
  
> [!NOTE]  
> Se la tabella viene pubblicata per la replica, è necessario apportare modifiche allo schema usando l'istruzione [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) di Transact-SQL oppure SMO (SQL Server Management Objects). Quando si apportano modifiche allo schema utilizzando Progettazione tabelle o Progettazione diagrammi di database, viene effettuato il tentativo di rimuovere e rigenerare la tabella. La modifica allo schema non riuscirà, poiché non è consentita la rimozione di oggetti pubblicati.  
  
## <a name="options"></a>Opzioni

**Vincolo CHECK selezionato**  
Elenca i vincoli CHECK disponibili. Per visualizzare le proprietà di un vincolo, selezionarlo nell'elenco.  
  
**Aggiungere**  
Crea un nuovo vincolo per la tabella di database selezionata, assegnandogli un nome predefinito e altri valori. Il vincolo diventerà attivo solo dopo che sarà stata immessa un'espressione.  
  
**Elimina**  
Rimuove dalla tabella il vincolo selezionato. Per annullare l'aggiunta di un vincolo CHECK, utilizzare questo pulsante per rimuovere il vincolo.  
  
**Categoria Generale**  
Viene espansa per visualizzare il campo della proprietà **Espressione** .  
  
**Espressione**  
Visualizza l'espressione relativa al vincolo CHECK selezionato. Per i nuovi vincoli, è necessario immettere l'espressione prima di uscire dalla casella. È anche possibile modificare vincoli CHECK esistenti. Per altre informazioni, vedere [Uso dei vincoli](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e).  
  
**Categoria Identità**  
Viene espansa per visualizzare le proprietà **Nome** e **Descrizione**.  
  
**Nome**  
Visualizza il nome del vincolo CHECK selezionato. Per modificare il nome del vincolo, digitare il testo direttamente nel campo della proprietà.  
  
**Descrizione**  
Descrive il vincolo CHECK. La descrizione può essere modificata digitando direttamente nel campo della proprietà oppure facendo clic sui puntini di sospensione ( **...** ) a destra del campo della proprietà e modificando il testo nella finestra di dialogo **Proprietà Descrizione**.  
  
**Categoria Progettazione tabelle**  
Viene espansa per visualizzare le proprietà **Verifica dati esistenti durante la creazione o la riabilitazione**, **Attiva per istruzioni INSERTS e UPDATES**e **Attiva per replica**.  
  
**Check Existing Data On Creation or Re-Enabling**  
Specifica se tutti i dati preesistenti, ovvero i dati presenti nella tabella prima della creazione del vincolo, vengono verificati in base al vincolo.  
  
**Attiva per istruzioni INSERTS e UPDATES**  
Specifica se il vincolo viene applicato quando i dati vengono inseriti o aggiornati nella tabella.  
  
**Applicare per replica**  
Indica se applicare il vincolo quando un agente di replica esegue un'inserimento o un aggiornamento in questa tabella.  
  
## <a name="see-also"></a>Vedere anche

[Utilizzo dei vincoli](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e)
[Finestra di dialogo Indici/chiavi &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/indexes-keys-dialog-box-visual-database-tools.md)
