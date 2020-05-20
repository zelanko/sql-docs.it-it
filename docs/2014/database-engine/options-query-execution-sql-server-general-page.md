---
title: Opzioni (esecuzione query-SQL Server-pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionGeneral
ms.assetid: 3f8d59bc-3f97-4e5d-8b86-5ac670d20780
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6d14371c1db5273d66fee327cc03d2b2e2de3edb
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000797"
---
# <a name="options-query-execution-sql-server-general-page"></a>Opzioni (esecuzione query-SQL Server-pagina generale)
  Utilizzare questa pagina per specificare le opzioni per l'esecuzione di query di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Le modifiche apportate a queste opzioni si applicano soltanto alle nuove query di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per modificare le opzioni per una query corrente, scegliere **Opzioni query** dal menu **Query** oppure fare clic con il pulsante destro del mouse nella finestra Query di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e scegliere **Opzioni query**.  
  
## <a name="options"></a>Opzioni  
 **SET ROWCOUNT**  
 Il valore predefinito 0 indica che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] rimarrà in attesa di risultati fino a quando non verranno ricevuti tutti i risultati. Specificare un valore maggiore di 0 se si desidera che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] interrompa la query dopo aver ottenuto il numero di righe specificato. Per disabilitare questa opzione in modo che vengano restituite tutte le righe, specificare SET ROWCOUNT 0.  
  
 **SET TEXTSIZE**  
 Il valore predefinito 2.147.483.647 byte indica che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornirà campi dati completi fino al limite dei campi dati `text` e `ntext`. Specificare un numero più piccolo per limitare i risultati in caso di valori elevati. Le colonne le cui dimensioni sono maggiori del numero specificato verranno troncate.  
  
 **Timeout esecuzione**  
 Consente di impostare il valore predefinito nella finestra di dialogo **Nuova connessione** . Usare questa casella di selezione per indicare a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] il numero di secondi di attesa prima dell'annullamento della query. Il valore 0 indica un'attesa infinita o nessun timeout. Questo valore è 0 in una nuova installazione.  
  
 **Separatore batch**  
 Consente di digitare una parola che verrà utilizzata per separare le istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] in batch. Il valore predefinito è GO.  
  
 **Per impostazione predefinita, apri le nuove query in modalità SQLCMD.**  
 Selezionare questa casella di controllo per aprire le nuove query in modalità SQLCMD. Per altre informazioni sulla modalità SQLCMD, vedere [Modifica di script SQLCMD con l'editor di query](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md).  
  
 Quando si seleziona questa opzione, tenere presente le limitazioni seguenti:  
  
-   Nell'editor di query del [!INCLUDE[ssDE](../includes/ssde-md.md)] , IntelliSense è disattivata.  
  
-   Poiché l'editor di query non è in esecuzione dalla riga di comando, non è possibile passare parametri della riga di comando, ad esempio variabili.  
  
-   Poiché l'editor di query non può rispondere ai prompt del sistema operativo, è necessario prestare attenzione a non eseguire istruzioni interattive.  
  
 **Ripristina predefiniti**  
 Fare clic su questo pulsante per reimpostare le impostazioni predefinite originali per tutti i valori della pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità sqlcmd](../tools/sqlcmd-utility.md)  
  
  
