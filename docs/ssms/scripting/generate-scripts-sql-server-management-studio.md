---
title: Generazione di script (SQL Server Management Studio)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: mathoma
ms.topic: conceptual
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: abdbbd7659221fb27df12ff03995b2d246241463
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253865"
---
# <a name="generate-scripts-sql-server-management-studio"></a>Generazione di script (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornisce due meccanismi per la generazione di script [!INCLUDE[tsql](../../includes/tsql-md.md)] . È possibile creare script per più oggetti usando la **Procedura guidata Genera e pubblica script**. È anche possibile generare uno script per un singolo oggetto o per più oggetti usando il menu **Crea script per** in **Esplora oggetti**.  

Per un'esercitazione dettagliata sulla creazione di script per diversi oggetti tramite SQL Server Management Studio (SSMS), vedere [Esercitazione: eseguire script per oggetti in SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/tutorials/scripting-ssms).

  
## <a name="before-you-begin"></a>Prima di iniziare  
 Scegliere il meccanismo che soddisfa maggiormente i requisiti.  
  
###  <a name="GenPubScriptWiz"></a> Procedura guidata Genera e pubblica script  
 Usare la **Procedura guidata Genera e pubblica script** per creare uno script [!INCLUDE[tsql](../../includes/tsql-md.md)] per molti oggetti. Durante la procedura guidata viene generato uno script di tutti gli oggetti contenuti in un database o un subset degli oggetti selezionati. La procedura guidata dispone di numerose opzioni per gli script, che consentono ad esempio di includere autorizzazioni, regole di confronto, vincoli e così via. Per istruzioni sull'uso della procedura guidata, vedere [Genera e pubblica script](../../relational-databases/scripting/generate-and-publish-scripts-wizard.md).  
  
###  <a name="OEScriptAsMenu"></a> Menu Crea script per in Esplora oggetti  
 Il menu **Script come** in Esplora oggetti consente di creare uno script per un solo oggetto, per più oggetti o per più istruzioni per un singolo oggetto. È possibile scegliere tra diversi tipi di script, per ad esempio creare, modificare o eliminare l'oggetto. È possibile salvare lo script in una finestra dell'editor di query, in un file o negli Appunti. Lo script viene creato in formato Unicode.  
  
##  <a name="ScriptSingleObject"></a> Per generare uno script per un singolo oggetto  
 **Per generare uno script per un singolo oggetto**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
  
2.  Espandere **Database**, quindi espandere il database che contiene l'oggetto per cui creare lo script.  
  
3.  Espandere la categoria dell'oggetto: ad esempio il nodo **Tabelle** o **Viste** .  
  
4.  Fare clic con il pulsante destro del mouse sull'oggetto e scegliere **Crea script per \<tipo di oggetto**, ad esempio **Crea script per tabella**.  
  
5.  Scegliere il tipo di script, ad esempio **Genera codice per istruzione CREATE** o **Genera codice per istruzione ALTER**.  
  
6.  Selezionare il percorso in cui salvare lo script, ad esempio **Nuova finestra editor di query** o **Appunti**.  

    ![Tabella script](media/generate-scripts-sql-server-management-studio/scripttable.png)
  
  
 È possibile usare il riquadro **Dettagli Esplora oggetti** per generare uno script per più oggetti della stessa categoria.  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
  
2.  Espandere **Database**, quindi espandere il database che contiene gli oggetti per cui creare lo script.  
  
3.  Espandere il nodo della categoria dei tipi di oggetto per cui si vuole creare uno script, ad esempio il nodo **Tabelle** .  
  
4.  Aprire il riquadro **Dettagli Esplora oggetti** premendo il tasto **F7**oppure selezionando **Dettagli Esplora oggetti** dal menu **Visualizza**.  
  
5.  Fare clic su uno degli oggetti per cui si desidera creare lo script.  
  
6.  Tenendo premuto CTRL fare clic sul secondo oggetto per cui si vuole creare lo script.  
  
7.  Fare clic con il pulsante destro del mouse su uno degli oggetti selezionati e scegliere **Crea script per \<tipo di oggetto>** .  

    ![Esplora oggetti](media/generate-scripts-sql-server-management-studio/objectexplorerdetails.png)
  
  
