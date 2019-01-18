---
title: Dipendenze tra oggetti | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.objectdependencies.f1
ms.assetid: c63d1160-3f3d-45df-99be-6fe081125fb5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fca3b535b31a3524389804442bb61370fb164008
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591535"
---
# <a name="object-dependencies"></a>Dipendenze tra oggetti
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Alcuni oggetti di database hanno dipendenze con altri oggetti di database. Le viste e le stored procedure dipendono ad esempio dall'esistenza di tabelle che contengono i dati restituiti dalla vista o dalla procedura. Nella finestra di dialogo **Dipendenze oggetto** della pagina Generale relativa all'oggetto corrente sono elencati sia gli oggetti di database necessari per il corretto funzionamento dell'oggetto in questione, sia gli oggetti che dipendono da tale oggetto. Un oggetto che fa riferimento a un altro oggetto nella propria definizione archiviata nel catalogo del sistema è definito *entità di riferimento*. Un oggetto a cui fa riferimento un altro oggetto è denominato *entità con riferimenti*.  
  
Nella finestra di dialogo **Dipendenze oggetto (pagina Avanzate)** per l'oggetto corrente sono elencati gli oggetti di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che dipendono dall'oggetto. È possibile che gli oggetti vengano archiviati in server diversi.  
  
Utilizzare questa finestra di dialogo per individuare le dipendenze prima di modificare o eliminare l'oggetto selezionato.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
**Oggetti dipendenti da** _\<oggetto selezionato>_  
Fare clic su questo pulsante per visualizzare un elenco di tutti gli oggetti registrati nelle dipendenze che dipendono dall'oggetto selezionato.  
  
**Oggetti da cui dipende** _\<oggetto selezionato>_ ****  
Fare clic su questo pulsante per visualizzare un elenco di tutti gli oggetti registrati nelle dipendenze da cui dipende l'oggetto selezionato.  
  
**Dipendenze**  
Se si fa clic su **Oggetti che dipendono da** *<selected object>* , vengono visualizzati in ordine gerarchico gli oggetti che dipendono dall'oggetto selezionato. Se si fa clic su **Oggetti da cui** **dipende** *<selected object>* vengono visualizzati in ordine gerarchico gli oggetti da cui l'oggetto selezionato dipende.  
  
**Nome**  
Consente di visualizzare il nome dell'oggetto selezionato nella visualizzazione albero **Dipendenze** precedente.  
  
**Tipo**  
Consente di visualizzare il tipo dell'oggetto selezionato nella visualizzazione albero **Dipendenze** precedente.  
  
**Data e ora ultima sincronizzazione**  
> [!NOTE]  
> Questa opzione è disponibile solo nella pagina **Avanzate** .  
  
Specifica l'ora e la data dell'ultimo aggiornamento delle informazioni relative alle dipendenze.  
  
**Tipo di dipendenza**  
> [!NOTE]  
> Questa opzione è disponibile solo nella pagina **Generale** .  
  
Consente di visualizzare il tipo di dipendenza tra due oggetti. I possibili valori sono i seguenti:  
  
-   Dipendenza associata a schema  
  
    È una relazione tra due oggetti che impedisce l'eliminazione o la modifica dell'oggetto a cui si fa riferimento finché esiste l'oggetto di riferimento. Una dipendenza associata a schema si ottiene quando viene creata una vista o una funzione definita dall'utente utilizzando la clausola WITH SCHEMABINDING, o quando una tabella fa riferimento a un altro oggetto tramite un vincolo CHECK o DEFAULT o nella definizione di una colonna calcolata.  
  
-   Dipendenza non associata a schema  
  
    È una relazione tra due oggetti che non impedisce l'eliminazione o la modifica dell'oggetto a cui si fa riferimento.  
  
-   Entità non disponibile o non risolta  
  
    Indica l'impossibilità di determinare il tipo di dipendenza. Si verifica solo quando l'oggetto selezionato si trova in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
